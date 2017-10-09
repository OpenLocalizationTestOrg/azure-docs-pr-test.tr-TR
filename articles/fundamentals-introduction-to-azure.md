---
title: aaaIntro tooMicrosoft Azure | Microsoft Docs
description: "Yeni tooMicrosoft Azure? Get hello temel bir bakış sunar nasıl yararlı örnekler ile Hizmetleri."
services: " "
documentationcenter: .net
author: rboucher
manager: carolz
editor: 
ms.assetid: 6f47f711-2208-4c21-8c1d-826a54c05c29
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2015
ms.author: robb
ms.openlocfilehash: 6791506abe813e19ca7b04d78d35cb46352a9028
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-microsoft-azure"></a>Microsoft Azure Tanıtımı
Microsoft Azure Microsoft'un uygulama için hello genel bulut platformudur.  Merhaba, bu makalenin, hakkında hiçbir şey bilmiyor olsanız da, Azure, hello temelleri anlamak için bir temel bulut toogive hedefidir.

**Nasıl tooread bu makalede**

Aşırı yüklenmiş kolay tooget olacak şekilde azure hello zaman artıyor.  Bu makalede ilk listelenir ve tooadditional Services'de Git hello temel hizmetlerini başlatın. Tek başına yalnızca hello ek hizmetler kullanamaz, ancak Azure'da çalışan bir uygulamanın hello çekirdek hello temel Hizmetleri oluşturan anlamına gelmez.

**Geri bildirim gönderin**

Görüşleriniz önemlidir. Bu makalede Azure etkili genel bakış vermesi gerekir. Yoksa, hello açıklamaları kısmında hello sayfanın hello bize bildirin. Bazı ayrıntı ne verin toosee ve nasıl tooimprove hello makale bekleniyordu.  

## <a name="hello-components-of-azure"></a>Merhaba bileşenleri, Azure
Azure Hizmetleri hello Yönetim Portalı ve hello gibi çeşitli görsel yardımlar kategorilere grupları [Azure bilgi grafiği nedir](https://azure.microsoft.com/documentation/infographics/azure/) . Merhaba Yönetim Portalı olduğundan, kullandığınız toomanage en (ancak tümünü değil) ile Azure Hizmetleri.

Bu makalede kullanacağı bir **farklı Kuruluş** tootalk hizmetleri hakkında temel alarak benzer işlevi ve toocall büyük olanları parçası olan önemli alt hizmetler.  

![Azure bileşenleri](./media/fundamentals-introduction-to-azure/AzureComponentsIntroNew780.png)   
 *Şekil: Azure Azure veri merkezlerinde çalışan Internet'ten erişilebilen uygulama hizmetleri sağlar.*

## <a name="management-portal"></a>Yönetim Portalı
Azure hello adında bir web arabirimi olan [Yönetim Portalı](http://manage.windowsazure.com) Yöneticiler sağlayan tooaccess ve çoğu, ancak tüm Azure özelliklerini yönetmek.  Microsoft genellikle daha eski bir devre dışı bırakmadan önce hello yeni UI portal Beta serbest bırakır. Merhaba daha yeni bir hello adlandırılır ["Azure Önizleme portalı"](https://portal.azure.com/).

Aynı zamanda hem portalları etkin olduğunda genellikle uzun bir çakışma yoktur. Çekirdek Hizmetleri her iki portallarında görünür, ancak tüm işlevselliği hem de kullanılabilir. Yeni hizmetler hello yeni portal ilk ve eski Hizmetleri'nde gösterebilir ve işlevsellik yalnızca hello eski olabilir.  Merhaba burada hello daha yeni ve tam tersini denetleyin hello eski Portalı'nda, bir değer bulamazsanız iletisidir.

## <a name="compute"></a>İşlem
Bulut platformu mu hello en temel şeyler uygulamalarını yürütmek biridir. Hello Azure işlem modellerinin her biri kendi rol tooplay sahiptir.

Bu teknolojiler ayrı ayrı kullanın veya bunları gerektiğinde olarak toocreate hello sağ foundation, uygulamanız için birleştirebilirsiniz. Seçtiğiniz bağlıdır hello yaklaşım hangi sorunları toosolve çalıştığınız.

### <a name="azure-virtual-machines"></a>Azure Sanal Makineler
![Azure sanal makineleri ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_VirtualMachinesIntroNew_12345.png)   
*Şekil: Azure sanal makineleri size hello bulutta sanal makine örnekleri üzerinde tam denetim.*

Standart bir görüntü veya birinden sağladığınız olup olmadığını hello özelliği toocreate isteğe bağlı olarak, bir sanal makine çok kullanışlı olabilir. Yaygın olarak altyapı (Iaas) olarak bilinen bu yaklaşım, Azure sanal makineleri sağladıkları olur. Şekil 2 gösterir bileşimini nasıl bir sanal makine (VM) çalışır ve nasıl bir VHD'den toocreate.  

bir VM toocreate, hangi VHD toouse ve hello VM'nin boyutunu belirtin.  Daha sonra VM çalıştıran bu hello hello süredir ödersiniz. Merhaba VHD kullanılabilir tutmak için bir en az depolama ücret olmasına rağmen hello dakika olarak ve yalnızca çalışırken, ücret ödersiniz. Azure hisse senedi önyüklenebilir bir işletim sistemi toostart gelen ("görüntüleri" olarak adlandırılır) VHD'ler Galerisi sunar. Bunlar Windows Server ve Linux, SQL Server, Oracle ve diğerleri gibi Microsoft ve ortak seçenekleri içerir. Ücretsiz toocreate VHD'leri ve görüntüler ve bunları kendiniz yükleyin. Hatta bunları çalışan Vm'leriniz erişmek ve yalnızca verileri içeren VHD karşıya yükleyebilirsiniz.

Merhaba VHD geldiği olduğunda, bir VM çalışırken yapılan tüm değişiklikler kalıcı olarak depolayabilirsiniz. Merhaba başlattığınızda bu VHD'den bir VM oluşturma şeyler kaldığınız yerden yukarı seçin. Merhaba geri sanal makineleri hello VHD'ler biz hakkında daha sonra konuşun Azure Storage bloblarında içinde depolanır.  Vm'leriniz toohardware ve disk hatası kayboluyor olmaz artıklık tooensure alma anlamına gelir. Ayrıca, olası toocopy hello VHD yerel olarak çalıştırma Azure dışında değiştirildi.

Uygulamanızı bir veya daha fazla sanal makinelerdeki nasıl olmadan önce oluşturduğu veya toocreate karar bağlı olarak, bu sıfırdan şimdi çalışıyor.

Bu oldukça genel yaklaşım toocloud computing kullanılan tooaddress birçok farklı sorunu olabilir.

**Sanal makine senaryoları**

1. **Geliştirme ve Test** -toocreate bunu kullanmayı bitirdiğinizde, bilgisayarı kapat bir uygun maliyetli geliştirme ve test platform kullanabilir. Ayrıca, hangi dilleri ve istediğiniz kitaplıkları kullanan uygulamaları çalıştırmak oluşturabilir ve. SQL Server ya da bir veya daha fazla sanal makinelerde çalışan başka bir DBMS toouse de seçebilirsiniz ve bu uygulamaların Azure sağlar hello veri yönetim seçeneklerinden herhangi birini kullanabilirsiniz.
2. **Uygulamaları tooAzure (yükseltme ve shift) taşıma** -"Yükseltme ve shift" başvuruyor toomoving uygulamanız çok forklift toomove büyük nesne kullanırken yaptığınız gibi.  "Yükseltme" yerel merkeziniz, VHD hello "tooAzure shift" ve orada çalıştırın.  Genellikle diğer sistemlerde bazı iş tooremove bağımlılıklar toodo da sahip olacaktır. Varsa çok seçenek 3 yerine tercih edebilirsiniz.  
3. **Veri merkeziniz genişletmek** -SharePoint veya diğer uygulamaları çalıştıran kullanım Azure VM'ler, şirket içi veri merkezinizin bir uzantısı olarak. toosupport Bu, Active Directory Azure Vm'lerde çalıştırarak olası toocreate Windows hello bulut etki alanlarında olan. Azure sanal (daha sonra belirtilen) ağ tootie yerel ağınızın ve ağınızdaki Azure'da birlikte kullanabilirsiniz.

### <a name="web-apps"></a>Web Apps
![Azure Web Apps ROBBCSIART_TEST](./media/fundamentals-introduction-to-azure/mscsiart_AzureWebsitesIntroNew_12345.png)   
 *Şekil: Azure Web uygulamaları bir Web sitesi uygulama hello bulutta toomanage hello temel web sunucusu olmadan çalışır.*

Web siteleri ve web uygulamalarını birini kişiler yapan hello en yaygın hello bulutta çalıştırılır. Azure sanal makineleri bu sağlar, ancak hala, bir veya daha fazla sanal makineleri ve işletim sistemleri için temel alınan hello yönetme hello sorumluluğu bırakır. Bulut Hizmetleri web rolleri bunu ancak dağıtma ve bunların Bakımı yönetimsel iş hala alır.  Ne yalnızca bir Web sitesi başka bir kişiye burada istediğiniz sizin için yönetimsel iş hello ilgilenir?

Bu, tam olarak Web Apps sağladıkları olur. Bu işlem modeli API'leri yanı sıra hello Azure yönetim portalını kullanarak bir yönetilen web ortamı sunar. Var olan bir Web sitesi uygulamasını Web uygulamalarına değişmeden taşıyabilir veya hello bulutta doğrudan yeni bir tane oluşturabilirsiniz. Bir Web sitesi çalışmaya başladıktan sonra ekleme ya da Azure Web Apps tooload Bakiye isteklerinde bağlı olan örneklerini dinamik olarak kaldırın. Azure uygulamaları, Web sitenizin bir sanal makinedeki diğer sitelerle çalıştığı, paylaşılan bir seçeneği ve kendi VM site toorun sağlayan standart bir seçenek sunar. Hello standart seçeneği ayrıca hello boyutunu (güç bilgisayar) gerekirse örneklerinizi artırmanıza olanak tanır.

Geliştirme için Web uygulamaları için ilişkisel depolama .NET, PHP, Node.js, Java ve Python SQL veritabanı ve MySQL'den (ClearDB, bir Microsoft iş ortağı) ile birlikte destekler. WordPress, Joomla ve Drupal gibi çeşitli popüler uygulamalar için yerleşik destek de sağlar. Merhaba tooprovide bir düşük maliyetli, ölçeklenebilir ve hello genel bulutunda Web sitelerini ve web uygulamaları oluşturmak için kapsamlı ve kullanışlı platform hedeftir.

**Web uygulamaları senaryoları**

Web uygulamaları hedeflenen toobe şirketler, geliştiriciler ve web tasarımı kurumları için yararlı olur. Şirketler için bu durum Web sitelerini çalıştırmak için bir kolay yönetmek, ölçeklenebilir, yüksek güvenlikli ve yüksek oranda kullanılabilir çözümüdür. Bir Web sitesi yukarı tooset gerektiğinde, Azure Web Apps ile en iyi toostart olduğundan ve kullanılabilir olmayan bir özellik ihtiyacınız sonra tooCloud Hizmetleri devam edin. Merhaba sonuna toochoose hello seçenekleri arasındaki yardımcı olabilecek daha fazla bağlantılar için hello "İşlem" bölümüne bakın.

### <a name="cloud-services"></a>Cloud Services
![Azure bulut hizmeti](./media/fundamentals-introduction-to-azure/CloudServicesIntroNew.png)   
*Şekil: Azure bulut Hizmetleri bir yerde toorun yüksek düzeyde ölçeklenebilir özel kod bir platformda hizmet (PaaS) ortamı olarak sağlar*

Toobuild çok sayıda eşzamanlı kullanıcıyı desteklemek, çok yönetim gerektirmez ve hiçbir zaman arıza bir bulut uygulaması istediğinizi varsayalım. Örneğin, bu kampanyanızın tooembrace hello bulut uygulamalarınızda birinin sürümünü oluşturma tarafından hizmet (SaaS) olarak yazılım bir yerleşik yazılım satıcısı olabilir. Veya hızlı büyüyecektir beklediğiniz bir tüketici uygulaması oluşturma başlangıç olabilir. Azure üzerinde oluşturuyorsanız, hangi yürütme modeli kullanmalısınız?

Bu tür bir web uygulaması oluşturma Azure Web Apps verir, ancak bazı kısıtlamalar vardır. İsteğe bağlı yazılımlar yükleyemezsiniz anlamına gelen yönetim erişimi, örneğin, sahip değilsiniz. Azure sanal makineleri size esneklik, yönetimsel erişim dahil olmak üzere çok sayıda ve bunu kesinlikle toobuild çok ölçeklenebilir bir uygulama kullanabilirsiniz, ancak, toohandle güvenilirlik ve yönetim pek çok görünüşünün kendiniz gerekir. Ne istiyorsunuz veren bir seçenek hello gerekir, ancak aynı zamanda güvenilirlik ve Yönetim için gerekli hello çalışmanın çoğu işleyen denetim olur.

Bu, tam olarak Azure bulut Hizmetleri tarafından sağlanan olur. Bu teknolojisi açıkça toosupport ölçeklenebilir, güvenilir ve düşük Yönetim uygulamaları tasarlanmış ve ne sık (PaaS) hizmet olarak Platform çağırdı örneği. toouse, seçtiğiniz, C#, Java, PHP, Python, Node.js veya başka bir şey gibi hello teknolojisini kullanan bir uygulama oluşturun. Kodunuzu daha sonra Windows Server sürümünü çalıştıran sanal makineler içinde (başvurulan tooas örnekler) yürütür.

Ancak bu Vm'lere hello Azure sanal makineler ile oluşturduğunuz olanları farklı. Tek şey, Azure için kendisini işletim sistemi düzeltme eklerini yükleme gibi şeyler yapmaktan bunları yönetir ve otomatik olarak yeni dağıtım, görüntüleri düzeltme eki uygulandı. Bu, uygulamanızın web veya çalışan rolü örnekleri durumda koruyun döndürmemelidir anlamına gelir; Bunun yerine, bir hello sonraki bölümde açıklanan hello Azure veri yönetimi seçenekleri de tutulmalıdır. Azure herhangi devreden yeniden, bu sanal makineleri de izler. Bulut ayarlayabilirsiniz Hizmetleri tooautomatically yanıt toodemand daha fazla veya daha az örneği oluşturun. Daha az kullanım olduğunda geri, kadar ödeme olmayan şekilde bu, artan toohandle kullanım ve ölçek sağlar.

İki rolleri toochoose bir örneğini oluştururken vardır, her ikisi de Windows Server tabanlı. Merhaba hello ikisi arasındaki temel fark, çalışan rolü örneği çalışmazken bir web rolü örneği IIS çalıştıran ' dir. Hem yönetilen hello aynı şekilde, ancak ve onu bir uygulama toouse için her iki ortak. Örneğin, bir web rolü örneği kullanıcılardan gelen istekleri kabul, sonra tooa çalışan rol örneği işleme için geçirin. tooscale uygulamanızın yukarı veya aşağı, Azure her iki rolün daha fazla örneğini oluşturmak veya var olan örneklerini kapatmak isteyebilir. Ve benzer tooAzure sanal makineler, size yalnızca hello süredir her web veya çalışan rolü örneğinin çalıştığından ücret ödersiniz.

**Senaryoları bulut Hizmetleri**

Bulut Hizmetleri hello platform Azure Web uygulamaları tarafından sağlanan daha fazla denetime ihtiyacınız fakat hello temel işletim sistemi üzerinde denetim gerek yoktur ideal toosupport büyük ölçeklendirme olur.

#### <a name="choosing-a-compute-model"></a>İşlem modeli seçme
Merhaba sayfa [Azure Web uygulamaları, bulut Hizmetleri ve sanal makineler karşılaştırması](app-service-web/choose-web-site-cloud-service-vm.md) daha ayrıntılı bilgi sağlar toochoose bir işlem modeli.

## <a name="data-management"></a>Veri Yönetimi
Uygulamaların veri ve farklı veri türleri farklı türdeki uygulamalar gerekir. Bu nedenle, Azure birkaç farklı şekilde toostore sağlar ve verileri yönetin. Çok sayıda depolama seçeneğinin Azure sağlar, ancak tüm çok dayanıklı depolama için tasarlanmıştır.  Bu seçeneklerin hiçbirini ile her zaman Azure veri merkezinde--Azure toouse coğrafi yedeklilik tooback tooanother datacenter en az 300 mil hemen yukarı izin verirseniz 6 arasında eşitlenmiş olarak saklanmasını verileriniz 3 kopyalar.     

### <a name="in-virtual-machines"></a>Sanal makineler
Merhaba özelliği toorun SQL Server ya da başka bir DBMS Azure sanal makineler ile oluşturulmuş VM'deki zaten belirtilmiş. Bu seçenek sınırlı toorelational sistemleri olmadığını unutmayın; Ayrıca, MongoDB ve Cassandra gibi ücretsiz toorun NoSQL teknolojileri de demektir. Kendi veritabanı sistemi çalıştırdığını BT basit çoğaltır ne ki tooin kendi veri merkezlerini kullanılan- ancak aynı zamanda bu DBMS hello yönetimini işleme gerektirir.  Diğer Seçenekler'de, sizin için hello yönetim tümünün veya daha fazla Azure işler.

Yeniden hello sanal makine hello durumunu ve oluşturun veya karşıya hiçbir ek veri diski (biz hakkında daha sonra konuşun) blob depolama birimi tarafından desteklenmektedir.  

### <a name="azure-sql-database"></a>Azure SQL Database
![Azure depolama SQL veritabanı](./media/fundamentals-introduction-to-azure/StorageAzureSQLDatabaseIntroNew.png)   

*Şekil: Azure SQL veritabanı yönetilen ilişkisel veritabanı hizmeti hello bulutta sağlar.*

İlişkisel depolama için Azure hello özelliği SQL veritabanı sağlar. Sizi kandırmaya Hello adlandırma izin vermeyin. Bu Windows Server üzerinde çalışan SQL Server tarafından sağlanan tipik bir SQL veritabanı farklıdır.  

SQL Azure adıysa, Azure SQL veritabanı hello tüm anahtar özellikleri atomik işlemleri dahil olmak üzere bir ilişkisel veritabanı yönetim sistemine, veri bütünlüğü, ANSI SQL sorguları ve tanıdık programlama ile birden çok kullanıcı tarafından eş zamanlı veri erişimi sağlar Model. SQL Server, SQL veritabanı Entity Framework kullanılarak erişilebilir gibi ADO.NET, JDBC ve tanıdık diğer veri teknolojileri erişin. Ayrıca, SQL Server Management Studio gibi SQL Server araçları ile birlikte T-SQL dili hello çoğunu destekler. Herkes için SQL Server (veya başka bir ilişkisel veritabanı) aşina SQL veritabanı kullanarak basittir.

Ancak SQL veritabanı değil yalnızca bir DBMS hello bulut BT PaaS hizmeti kullanıcının. Hala verilerinizi ve kimlerin erişebileceğini denetlemek, ancak SQL veritabanı hello donanım altyapısını yönetme ve otomatik olarak hello veritabanı ve işletim sistemi yazılımını toodate kurma tutma gibi hello yönetim grunt iş ilgilenir. SQL veritabanı aynı zamanda yüksek kullanılabilirlik sağlar, otomatik yedeklemeler, zaman içinde nokta geri yükleme ve kopya coğrafi bölgeler arasında çoğaltabilirsiniz.  

**SQL veritabanı için senaryolar**

İlişkisel depolama gerektiren (Merhaba işlem modellerinden herhangi biri kullanılarak) bir Azure uygulaması oluşturuyorsanız, SQL veritabanı iyi bir seçenek olabilir. Vardır; bu nedenle diğer senaryolar bolca dış hello bulut çalışan uygulamalar da bu hizmet, yine de kullanabilirsiniz. Örneğin, SQL veritabanında depolanan verileri Masaüstü, dizüstü bilgisayarlar, tabletler ve telefonlar gibi farklı istemci sistemlerden erişilebilir. Ve yerleşik yüksek kullanılabilirlik çoğaltması aracılığıyla sağladığından, SQL veritabanı kullanarak kapalı kalma süresini en aza indirmenize yardımcı olabilir.

### <a name="tables"></a>Tablolar
![Azure depolama tabloları](./media/fundamentals-introduction-to-azure/StorageTablesIntroNew.png)  

*Şekil: Azure tabloları düz bir NoSQL şekilde toostore verileri sağlar.*

Bu özellik farklı koşulları kaydının parçası "Azure depolama" olarak adlandırılan daha büyük bir özellik olarak da adlandırılır. "Tablo", "Azure tabloları" veya "depolama tabloları" görürseniz, tüm hello aynı anlama.  

Ve hello adıyla kafası yok: Bu teknoloji ilişkisel depolama sağlamaz. Aslında, bu bir anahtar/değer deposu olarak adlandırılan bir NoSQL yaklaşım örneğidir. Azure tabloları dize, tamsayı ve tarihleri gibi çeşitli türlerdeki özelliklerini depolamak bir uygulama sağlar. Bir uygulama, bu grubu için benzersiz bir anahtar sağlayarak bir grup özellik sonra alabilirsiniz. While karmaşık işlemleri birleştirmeler desteklenmez gibi hızlı erişim tootyped veri tabloları sunar. Bunlar ayrıca olabildiğince çok miktarda veri terabayt tek tablo mümkün toohold çok ölçeklenebilir. Ve bunların Basitlik eşleşen, tablolar SQL veritabanının ilişkisel depolama daha genellikle daha ucuz toouse.

**Tablolar için senaryolar**

Toocreate istediğinizi düşünelim hızlı gereken Azure uygulaması tootyped veri olabilir, çok sayıda erişim ancak tooperform karmaşık SQL sorgularını bu verilere ihtiyaç duymaz. Örneğin, her kullanıcı için toostore müşteri profil bilgileri gerektiren bir tüketici uygulaması oluşturduğunuzu düşünün. Uygulamanızı toobe çok popüler için çok fazla veri tooallow gerekir, ancak bu veriler, depolama ötesinde ile basit şekilde alma olmaz şekilde geçiyor. Bu tam olarak hello Azure tabloları mantıklı olduğu senaryo türüdür.

### <a name="blobs"></a>Bloblar
![Azure Storage Bloblarında](./media/fundamentals-introduction-to-azure/StorageBlobsIntroNew.png)    
*Şekil: Azure BLOB'ları yapılandırılmamış ikili veriler sağlar.*  

Azure BLOB'ları ("Blob Depolama" ve "Depolama BLOB'lar" yalnızca hello yeniden olan aynı anlama) tasarlanmış toostore olan yapılandırılmamış ikili veriler. Tablolar gibi BLOB'lar uygun maliyetli depolama sağlar ve tek bir blob 1 TB (bir terabayt) büyük olabilir. Azure uygulamalarını, bir Azure örneği bağlanan bir Windows dosya sistemi için kalıcı depolama sağlama BLOB'lar olanak sağlayan Azure sürücüler de kullanabilirsiniz. Normal Windows dosyalar Hello uygulamayı görür ancak hello içeriği gerçekte bir blob'a depolanır.

BLOB storage (sanal makineler dahil) diğer Azure, birçok özellik tarafından kullanılan, kesinlikle iş yüklerinizi çok işleyebilmesi için.

**BLOB'lar için senaryolar**

Video, büyük dosyalar veya diğer ikili bilgilerini depolayan bir uygulama için basit, ucuz depolama BLOB'ları kullanabilirsiniz. BLOB'ları de yaygın olarak, biz hakkında daha sonra konuşur içerik teslim ağı gibi diğer hizmetler ile birlikte kullanılır.  

### <a name="import--export"></a>İçeri Aktarmak / Dışarı Aktarmak
![Azure alma dışarı aktarma hizmeti](./media/fundamentals-introduction-to-azure/ImportExportIntroNew.png)  

*Şekil: Azure alma / verme fiziksel bir sabit sürücü tooor azure'dan daha hızlı ve ucuz toplu veri içeri veya dışarı aktarma için hello özelliği tooship sağlar.*  

Bazen toomove çok miktarda veri Azure'da istersiniz. Uzun, belki de gün sürebilir ve çok miktarda bant genişliği kullanın. Bu durumda, Azure içeri/sağlayan, tooship Bitlocker şifrelenmiş 3,5" SATA sabit sürücü doğrudan tooAzure veri merkezleri, burada Microsoft hello verileri blob depolama alanına sizin için aktaracak dışarı aktarma, kullanabilirsiniz.  Merhaba karşıya yükleme tamamlandıktan sonra Microsoft hello sürücüleri geri tooyou gelir.  Ayrıca, büyük miktarlarda verileri Blob depolama biriminden sabit sürücüleri dışarı aktarılabilir ve posta aracılığıyla geri tooyou gönderilen olduğunu isteyebilir.

**Senaryoları için İçeri Aktar / dışarı aktarma**

* **Büyük veri geçişi** - büyük miktarda veriyi (terabayt) sahip herhangi bir zamanda tooupload tooAzure istediğiniz, hello içeri/dışarı aktarma hizmeti olan genellikle çok daha hızlı ve hello aktarılması daha ucuz belki de Internet. BLOB'ları Hello veri olduktan sonra tablo depolamaya veya bir SQL veritabanı gibi diğer formları içine işleyebilir.
* **Arşivlenen veri kurtarma** -içeri/dışarı aktarma toohave Microsoft aktarımı büyük miktarlarda veri göndermek ve bu aygıt sahip tooa depolama aygıtı teslim geri tooa konumu istediğiniz Azure Blob depolama alanına depolanır kullanabilirsiniz. Bu biraz zaman alır çünkü olağanüstü durum kurtarma için iyi bir seçenek değil. Hızlı erişim gerekmeyen arşivlenmiş veriler için en iyisidir.

### <a name="file-service"></a>Dosya hizmeti
![Azure dosya hizmeti](./media/fundamentals-introduction-to-azure/FileServiceIntroNew.png)    
*Şekil: Azure Dosya Hizmetleri SMB sağlar \\ \\server\share yolları hello bulutta çalışan uygulamalar için.*

Şirket içi, ortak toohave büyük miktarlarda dosya depolama hello sunucu ileti bloğu (SMB) protokolü kullanılarak üzerinden erişilebilir olan bir \\ \\Server\share biçimi. Azure, hello buluta bu protokolü toouse sağlayan bir hizmet artık sahiptir. Azure'da çalışan uygulamalar hakkında bilgi sahibi dosya sistemi ReadFile ve WriteFile gibi API'leri kullanarak VM'ler arasında tooshare dosyaları kullanabilirsiniz. Ayrıca, hello dosyaları da hello erişilebilen aynı anda bir sanal ağ da ayarladığınızda sağlayan tooaccess hello paylaşımları şirket içi bir REST arabirimi aracılığıyla. Azure dosyaları hello blob hizmeti üstünde oluşturulmuş, aynı kullanılabilirlik, dayanıklılık, ölçeklenebilirlik ve coğrafi artıklık Azure depolama alanına yerleşik devralır şekilde hello.

**Azure dosyaları için senaryolar**

* **Geçirme mevcut uygulamaları toohello bulut** -dosyasını kullanan kendi daha kolay toomigrate şirket içi uygulamalar toohello bulut hello uygulama bölümleri arasında tooshare veri paylaşır. Her VM toohello dosya paylaşımı bağlanır ve ardından onu okuyabilir ve bir şirket içi dosya karşı paylaştığınız gibi dosyaları yazma.
* **Uygulama ayarları paylaşılan** -dağıtılmış uygulamalar için genel bir desen toohave yapılandırma dosyaları burada bunlar erişilebilir birçok farklı sanal makinelerden merkezi bir konumda olduğundan. Bu yapılandırma dosyalarını bir Azure dosya paylaşımında depolanan ve tüm uygulama örnekleri tarafından okunur. Hello ayarları da toohello yapılandırma dosyalarını dünya çapında erişime hello REST arabirimi, yönetilebilir.
* **Tanılama paylaşımı** - kaydetme ve tanılama dosyalarında günlükler, ölçümler gibi paylaşma ve kilitlenme dökümleri. Bu dosyalar hello SMB ve REST arabirimi kullanılabilir olan uygulamalar toouse çeşitli işleme ve hello tanılama verilerini çözümleme analiz araçları sağlar.
* **Geliştirme/Test/Debug** - hello bulutta sanal makinelerde geliştiriciler veya Yöneticiler çalışırken sık sık ihtiyaç duydukları birtakım Araçlar ve yardımcı programlar. Yükleme ve her sanal makinede bu yardımcı programları dağıtmak zaman alıcıdır. Azure dosyaları ile geliştirici veya yönetici kendi sık kullandığınız araçları bir dosya paylaşımında depolayabilir ve herhangi bir sanal makineden toothem bağlanın.

## <a name="networking"></a>Ağ
Azure Merhaba dünya genelinde yaygın birçok veri merkezleri bugün çalıştırır. Bir uygulamayı çalıştırmak veya veri depolamak, bir veya daha fazla bu veri merkezlerinde toouse seçebilirsiniz. Aşağıdaki hizmetlerden hello kullanarak çeşitli şekillerde toothese veri merkezleri da bağlanabilirsiniz.

### <a name="virtual-network"></a>Sanal Ağ
![VirtualNetwork](./media/fundamentals-introduction-to-azure/VirtualNetworkIntroNew.png)   

*Şekil: Sanal ağlar sağlar hello bulut özel bir ağda farklı hizmetler tooeach iletişim kurabilirsiniz şekilde diğer veya tooon içi kaynaklara VPN şirketler arası bağlantı kurma ayarlarsanız.*  

Bir kullanışlı bir yol toouse genel bulut tootreat olduğundan, kendi veri merkezinizin bir uzantısı olarak.

İsteğe bağlı VM'ler oluşturabileceğinden, sonra bunları kaldırmak (ve ödeme Durdur) bunlar artık gerekmediğinde, yalnızca istediğinizde gücünün olabilir. Ve Azure sanal makineler, SharePoint, Active Directory ve diğer tanıdık şirket içi yazılım çalışan sanal makineler oluşturmanıza olanak tanır olduğundan, bu yaklaşım zaten hello uygulamaları ile çalışabilirsiniz.

toomake Bu, kendi veri merkezinizde çalışıyormuş gibi gerçekten yararlı olsa, kullanıcılarınızın toobe mümkün tootreat bu uygulamaları gelmelidir. Bu, tam olarak hangi Azure Virtual Network sağlar olur. Bir VPN ağ geçidi cihazı kullanarak, bir yönetici, yerel ağınız ve Azure sanal ağında dağıtılan tooa Vm'leriniz arasında bir sanal özel ağ (VPN) ayarlayabilirsiniz. Kendi IP v4 adresi toohello bulut VM'ler atamak için kendi ağ üzerindeki toobe görünürler. Kuruluşunuzdaki kullanıcıların bu VM'lerin hello uygulamaları erişebilir, yerel olarak çalışıyormuş gibi içerir.

Planlama ve uygun bir sanal ağ oluşturma hakkında daha fazla bilgi için bkz: [sanal ağ](virtual-network/virtual-networks-overview.md).

### <a name="express-route"></a>Express Route
![ExpressRoute](./media/fundamentals-introduction-to-azure/ExpressRouteIntroNew.png)   

*Şekil: ExpressRoute kullanan bir Azure sanal ağı, ancak yolları bağlantılarında daha hızlı satırları yerine ayrılmış genel Internet hello.*  

Daha fazla bant genişliği ya da Azure sanal bağlantı sağlayan ağ güvenlikten gerekiyorsa, ExpressRoute bakabilirsiniz. Bazı durumlarda, ExpressRoute de tasarruf. Azure sanal ağında hala gerekir, ancak Azure ile siteniz arasında hello bağlantısını kullanan hello geçmez adanmış bir bağlantı genel Internet. Bu hizmet toouse sipariş, bir ağ hizmeti sağlayıcısı veya bir exchange sağlayıcısı sahip bir anlaşma toohave gerekir.

Bir ExpressRoute bağlantısı ayarlama daha fazla süresi gerektirir ve planlama toostart isteyebilirsiniz şekilde, bir siteden siteye VPN ile sonra tooan ExpressRoute bağlantısı geçirme.

ExpressRoute hakkında daha fazla bilgi için bkz: [ExpressRoute teknik genel bakış](expressroute/expressroute-introduction.md).

### <a name="traffic-manager"></a>Traffic Manager
![TrafficManager](./media/fundamentals-introduction-to-azure/TrafficManagerIntroNew.png)   

*Şekil: Azure trafik Yöneticisi akıllı kurallarına göre tooroute genel trafiği tooyour hizmeti sağlar.*

Azure uygulamanız birden çok veri merkezlerinde çalıştığından, kullanıcıların Azure Traffic Manager tooroute isteklerini hello uygulama örneklerinde akıllıca kullanabilirsiniz. Trafiği yönlendirmek erişilebilir olduğu sürece Azure üzerinde çalışmayan tooservices hello Internet.  

Bir Azure uygulamasıyla Merhaba Dünya yalnızca tek bir parçası olarak kullanıcılar yalnızca bir Azure veri merkezinde çalıştırabilirsiniz. Kullanıcıların uygulamayla Merhaba dünya genelinde ancak dağılmış, veri merkezlerinde birden çok, büyük olasılıkla toorun belki bile bunların tümünün. Bu ikinci durumda, bir sorun yüz: nasıl, akıllıca doğrudan kullanıcılar tooapplication örnekleri? Büyük olasılıkla kendi hello en iyi yanıt süresi verecektir beri hello süreyi en büyük olasılıkla her kullanıcı tooaccess hello datacenter en yakın tooher, istediğiniz. Ancak ne hello uygulama örneğini aşırı yüklenmiş veya kullanılamaz olur? Bu durumda, misiniz iyi toodirect her isteği otomatik olarak olması tooanother datacenter. Bu, tam olarak hangi Azure trafik Yöneticisi tarafından yapılır olur.

bir uygulama Hello sahibi kullanıcıların isteklerini yönlendirilmiş toodatacenters nasıl gerektiğini belirtin ve ardından bu kurallar giden trafik Yöneticisi toocarry dayanan kuralları tanımlar. Örneğin, kullanıcıların yönlendirilmiş toohello en yakın Azure veri merkezi normalde olabilir, ancak kendi varsayılan veri merkezini hello yanıt süresi diğer veri merkezleri hello yanıt süresi aştığında tooanother bir gönderilen. Çok sayıda kullanıcı içeren genel dağıtılmış uygulamalar için bir yerleşik hizmet toohandle sorunlarınız bu gibi yararlıdır.

Trafik Yöneticisi dizin adı hizmeti (DNS) tooroute kullanıcılar tooservice uç noktaları kullanır ancak bu bağlantı yapıldıktan sonra daha fazla trafiği trafik Yöneticisi ile geçmez. Bu trafik Yöneticisi, hizmet iletişimleri yavaşlatabilir bir performans sorunu engeller.

## <a name="developer-services"></a>Geliştirici Hizmetleri
Azure Araçları toohelp geliştiriciler sunar ve BT Uzmanı oluşturup hello bulutta uygulamalarını.  

### <a name="azure-sdk"></a>Azure SDK
Geri 2008'de hello Azure ilk yayım öncesi sürümü yalnızca .NET development desteklenir. Bugün, Bununla birlikte, Azure uygulamalarını neredeyse herhangi bir dilde oluşturabilirsiniz. Microsoft, şu anda .NET, Java, PHP, Node.js, Ruby ve Python için dile özgü SDK'ları sağlar. C++ gibi herhangi bir dil için temel destek sağlayan genel bir Azure SDK yoktur.  

Bu SDK'ları oluşturmak, dağıtmak ve Azure uygulamaları yönetmenize yardımcı olur. Ya da kullanılabilir gelen [www.microsoftazure.com](https://azure.microsoft.com/downloads/) veya GitHub ve Visual Studio ve Eclipse ile kullanılabilir. Azure Ayrıca, geliştiricilerin uygulamaları tooAzure Linux ve Macintosh sistemlerden dağıtmak için araçlar da dahil olmak üzere tüm Düzenleyicisi veya geliştirme ortamı ile kullanabileceğiniz komut satırı araçları sunar.

Azure uygulamalar oluşturmanıza yardımcı yanı sıra bu SDK'ları da yardımcı istemci kitaplıkları, yazılım oluşturmak sağlamak Azure hizmetlerini kullanır. Örneğin, okuyan ve Azure BLOB'ları yazan bir uygulama oluşturmak veya hello Azure Yönetimi arabirimi aracılığıyla Azure uygulamalarını dağıtan bir aracı oluşturun.

### <a name="visual-studio-team-services"></a>Visual Studio Team Services
Visual Studio Team Services hello Azure toodevelop uygulamalarda yardımcı olan bir sayı Hizmetleri kapsayan pazarlama bir addır.

tooavoid karışıklığı -, Visual Studio barındırılan veya Web tabanlı bir sürümü sağlamaz. Visual Studio çalışan yerel kopyasını yine gerekir. Ancak, çok yararlı olabilecek diğer birçok araçlar sağlar.

Sürüm denetimi ve iş öğesi izleme sunar Team Foundation Service adlı bir barındırılan kaynak denetim sistemi içermez.  Tercih ederseniz, Git sürüm denetimi için bile kullanabilirsiniz. Ve project tarafından kullandığınız hello kaynak denetim sistemi değişebilir. Sınırsız özel takım projeleri erişilebilen herhangi bir yere hello world oluşturabilirsiniz.  

Visual Studio Team Services yük test etme hizmeti sağlar. Visual Studio vm'lerde hello bulutta oluşturulan yük testlerini çalıştırabilirsiniz. Merhaba tooload test ile istediğiniz kullanıcıları toplam sayısını belirtin ve Visual Studio Team Services otomatik olarak kaç aracıları gerekli belirlemek, gerekli hello sanal makineleri Döndür ve yük testleri yürütün. MSDN abone değilseniz, her ay sınama yük boş kullanıcı dakika binlerce alın.

Visual Studio Team Services aynı zamanda sürekli tümleştirme derlemeler gibi özellikleri, Kanban panolarına ve sanal takım odaları Çevik Geliştirme desteği sağlar.

**Visual Studio Team Services senaryoları**

Visual Studio Team Services toocollaborate dünya çapında ihtiyaç ve zaten hello altyapısına yer toodo şekilde sahip olmayan şirketler için iyi bir seçenektir. Dakika cinsinden Kurulum alın, kaynak denetim sistemi seçin ve kod yazma ve o gün oluşturmaya başlayın.  Hello team araçları yer için eşgüdüm sağlar ve işbirliği ve hello ek araçlar tootest hello analiz gereken sağlamak ve uygulamanızı hızlı bir şekilde ayarlamak.

Ancak daha verimli olması durumunda zaten bir şirket içi sistem olan kuruluşlar yeni Visual Studio Team Services toosee projelerde test edebilirsiniz.   

### <a name="application-insights"></a>Application Insights
![Application Insights](./media/fundamentals-introduction-to-azure/ApplicationInsights.png)  

*Şekil: Application Insights izleyiciler performans ve kullanım canlı web veya aygıt uygulamanızın.*

Mobil aygıtlar, masaüstü bilgisayarlar veya web tarayıcıları - çalıştırıldığını - uygulamanızı yayımladıysanız, Application Insights nasıl çalıştığını ve hangi kullanıcıların ile yaptıklarını söyler. Kilitlenmeler ve yavaş yanıt sayısını tutar, uyarı, hello rakamları kabul edilemez eşikleri arası ve yardımcı sorunların tanılanmasına.

Yeni bir özellik geliştirirken toomeasure başarısını kullanıcılarla planlayın. Kullanım modelleri analiz etme tarafından ne müşterileriniz için en iyi çalıştığını anlamak ve her geliştirme döngüsü uygulamanızı geliştirin.

Azure üzerinde barındırılan rağmen uygulamalar, hem şirket hem de Azure dışı geniş ve artan bir dizi için Application Insights çalışır. J2EE ve ASP.NET web uygulamaları kapsanan, yanı sıra iOS, Android, OSX ve Windows uygulamaları. Telemetri gönderilen hello uygulamasıyla, yerleşik bir SDK toobe analiz ve Application Insights hizmeti azure'da hello görüntülenir.

Daha fazla özel analytics istiyorsanız, hello telemetri akışı tooa veritabanı veya tooPower BI veya diğer araçlar verin.

**Uygulama Öngörüler senaryoları**

Bir uygulama geliştirmektedir. Bir web uygulaması veya bir aygıt uygulama veya cihaz uygulaması web arka ucuna sahip olabilir.

* Yayımlandıktan sonra uygulamanızın hello performansı ayarlamak ya da test olarak kullanılırken yükleyin.  Application Insights telemetri tüm yüklü hello örneklerden toplar ve yanıt sürelerini, istek ve özel durum sayısı, bağımlılık yanıt sürelerini ve diğer performans göstergelerini grafiklerle sunar. Bu, uygulamanızın performansı ayarlamak yardımcı olur. Kod tooreport ekleyebilmeniz için gerekirse daha spesifik veriler.
* Algılama ve canlı uygulamanızdaki sorunları tanılayın. Kabul edilebilir eşikleri performans göstergelerini arası, e-posta ile uyarıları alabilirsiniz. Belirli kullanıcı oturumları, örneğin bir özel duruma neden olan toosee hello isteği araştırabilirsiniz.
* Kullanım tooassess hello her yeni özellik başarısını izleyebilirsiniz. Yeni kullanıcı hikayesi tasarlarken, toomeasure ne kadar kullanılır ve olup kullanıcıların beklenen hedeflerine ulaşması planlayın. Application Insights, web sayfası görünümleri gibi temel kullanım verilerini verir ve kod tootrack hello kullanıcı deneyimi daha ayrıntılı olarak ekleyebilirsiniz.

### <a name="automation"></a>Otomasyon
Hiç kimse hello yapılması toowaste zaman yöntemlerine aynı el ile tekrar tekrar işler. Azure Otomasyonu bir yöntem sunar, toocreate için izleme, yönetme ve kaynakları Azure ortamınızda dağıtın.  

Otomasyon Windows PowerShell iş akışları (ve yalnızca normal PowerShell) kullanan "runbook'lar" Merhaba perde arkasında kullanır. Runbook'ları, kullanıcı etkileşimi olmadan yürütülen toobe yöneliktir. PowerShell iş akışları sağlar hello boyunca kontrol noktaları, kaydedilmiş bir komut dosyası toobe hello durumunu yolu. Bir hata oluşursa, bir komut dosyası hello başından toostart sahip değilsiniz. Merhaba son denetim noktası onu yeniden başlatabilirsiniz. Bu çok fazla olası her hata toomake hello betik işleyici çalışırken iş kaydeder.

**Otomasyon senaryoları**

Azure Otomasyonu iyi seçimdir tooautomate hello el ile uzun süreli, hatasız ve sık tekrarlanan görevleri Azure içindir.

### <a name="api-management"></a>API Management
Oluşturma ve uygulama programlama arabirimleri (API) yayımlama hello üzerinde Internet yaygın bir şekilde tooprovide Hizmetleri tooapplications olmasıdır. Bu Hizmetleri (örneğin, hava durumu verileri) satılabilir varsa, bir kuruluşun diğer üçüncü tarafların izin verebilir tooaccess, bu aynı Hizmetleri için bir ücret. Toomore ortakları ölçeklendirmenize göre genellikle toooptimize gerekir ve erişimi denetlemek.  Bazı iş ortakları bile hello verileri farklı bir biçimde gerekebilir.

Azure API Management, kuruluşların toopublish API'leri toopartners, çalışanlar ve üçüncü taraf geliştiriciler için güvenli bir şekilde ve ölçekte kolaylaştırır. Bir proxy toocall hello gibi gerçek uç noktası, dönüştürme, önbelleğe alma gibi hizmetleri sağlarken davranır kısıtlamayı, erişim denetimi ve analiz toplama ve farklı bir API uç noktası sağlar.

**API yönetim senaryoları**

Şirketiniz tüm Örneğin, her kamyon hello yolda aygıtları olan sevkiyat şirket toocall geri tooa Merkezi hizmeti tooget verilerini--gereken cihazların ayarlanmış varsayalım.  Merhaba şirket tooset kesinlikle istersiniz, güvenilir bir şekilde tahmin etmek ve güncelleştirme teslimat saatleri verebilmesi sistem tootrack kendi kamyonlar öyledir. Bu, sahip kaç kamyonlar bilmeniz ve uygun şekilde planlamanız.  Her kamyon merkezi bir konum tooa, konumlandırma ve hız veriler ve belki de daha fazla ile geri çağıran bir aygıtı gerekir.

Bir müşterinin şirket sevkiyat hello büyük olasılıkla misiniz konumlandırma bu veri alma de yararlanabilir.  Merhaba müşteri burada bunlar, ne kadar bunlar (ne bunlar tooship Ücretli ile birleştirilmiş varsa) belirli yollar ödeme takılı ürünleri tootravel, ne kadar yüklü tooknow kullanabilirsiniz. Şirket sevkiyat hello zaten bu veriler toplar, birçok müşteri için ödeme.  Ancak daha sonra şirket sevkiyat hello tooprovide veri toogive müşteriler hello bir yol gerekiyor. Bunlar erişim toocustomers sağladığınızda, ne sıklıkta hello veri sorgulanan üzerinde denetim olmayabilir. Bunlar, hangi verilerin erişebilecek kişileri hakkında tooprovide kuralları sahip olur. Bu kuralların hepsi kendi API'nin yerleşik toobe gerekir. API Management burada yardımcı olabilecek budur.  

## <a name="identity-and-access"></a>Kimlik ve Erişim
Kimliğine sahip çalışan çoğu uygulamayı bir parçasıdır. Kimin bir kullanıcı bilerek bu kullanıcı ile nasıl etkileşim kurması gerektiğine karar bir uygulama sağlar. Azure Hizmetleri toohelp parça kimliği sağlar yanı sıra zaten kullanıyor olabileceğiniz kimlik depolarına ile tümleştirin.

### <a name="active-directory"></a>Active Directory
Çoğu Dizin Hizmetleri gibi Azure Active Directory Kullanıcıları ve ait oldukları hello kuruluşlar hakkında bilgi depolar. Oturum açmasına olanak tanır, ardından, onları tedarik belirteçleri ile bunların tooapplications tooprove kimliklerini sunabilir. Ayrıca, Windows Server Active Directory'yle yerel ağınıza çalışan kullanıcı bilgileri eşitleme sağlar. Merhaba mekanizmaları ve Azure Active Directory tarafından kullanılan veri biçimleri ile Windows Server Active Directory'de kullanılanlarla aynı değildir, ancak hello işlevler gerçekleştirdiği oldukça benzer.

Azure Active Directory bulut uygulamaları tarafından birincil olarak kullanılmak üzere tasarlanmıştır, önemli toounderstand. Örneğin veya diğer bulut platformlarda Azure üzerinde çalışan uygulamalar tarafından kullanılabilir. Ayrıca, Office 365'te olanlar gibi Microsoft'un kendi bulut uygulamaları tarafından kullanılır. Ancak, Azure sanal makineler ve Azure Virtual Network kullanarak hello bulutunu merkeziniz tooextend istiyorsanız, Azure Active Directory hello doğru seçim değildir. Bunun yerine, Windows Server Active Directory sanal makinelerde toorun isteyeceksiniz.

toolet uygulamaları içerdiği hello bilgilere erişebilir, Azure Active Directory RESTful bir Azure Active Directory grafik API'si sağlar. Bu API, tüm platform erişim dizin nesneleri ve aralarındaki ilişkiler hello üzerinde çalışan uygulamalar sağlar.  Örneğin, yetkili bir uygulama bu API toolearn bir kullanıcı, ait hello grupları ve diğer bilgileri hakkında kullanabilir. Uygulamaları bunları hello bağlantıları kişiler arasında daha akıllıca çalışmak grafik veren kullanıcılar their sosyal arasındaki ilişkileri de görebilirsiniz.

Başka bir özelliği, bu hizmet, Azure Active Directory erişim denetimi, bir uygulama tooaccept kimlik bilgilerini Facebook, Google, Windows Live ID ve diğer popüler kimlik sağlayıcılardan kolaylaştırır. Merhaba uygulama toounderstand hello farklı veri biçimleri ve her bu sağlayıcıları tarafından kullanılan protokoller istemeden yerine, erişim denetimi bunların tümünü tek bir ortak biçimine çevirir. Ayrıca, bir veya daha fazla Active Directory etki alanı oturum açmayı kabul bir uygulama sağlar. Örneğin, bir SaaS uygulaması sağlayan bir satıcı Azure Active Directory erişim denetimi toogive kullanıcıların her müşterilerin tek oturum açma toohello uygulamasını kullanabilirsiniz.

Dizin Hizmetleri, bilgi işlem içi çekirdek masaüstünün oluşturulur. Bunlar ayrıca hello bulutta önemli olduğunu şaşırtıcı olmamalıdır.

### <a name="multi-factor-authentication"></a>Multi-Factor Authentication
![Azure Multi-Factor Authentication](./media/fundamentals-introduction-to-azure/MFAIntroNew.png)   

*Şekil: Çok faktörlü kimlik doğrulaması hello işlevselliği, uygulama tooverify için birden fazla form tanımı sağlar*

Güvenlik her zaman önemlidir. Çok faktörlü kimlik doğrulaması (MFA) yalnızca kullanıcıların kendilerini hesaplarına erişim güvence altına yardımcı olur. MFA (olarak da bilinen iki öğeli kimlik doğrulama veya "2FA") kullanıcılara iki kimlik doğrulama kullanıcı oturum açmaları ve işlemleri için bu üç yöntem sağlamanız gerekir.

* (Genellikle parola) bildiğiniz bir şey
* (Kolayca, bir telefon gibi yineleniyor değil güvenilir bir cihaz) sahip olduğunuz şey
* (Biyometri) olan bir şey

Bir kullanıcı oturum açtığında gerektirebilir şekilde tooalso bir mobil uygulama, bir telefon araması veya SMS mesajı parolalarını birlikte kimliğini doğrulayın. Varsayılan olarak, Azure Active Directory kullanıcı oturum açma işlemleri için yalnızca kimlik doğrulama yöntemi olarak hello parolaların kullanımını destekler. MFA SDK kullanarak dizinleri hello ve MFA Azure AD ile birlikte veya özel uygulamaları ile kullanabilirsiniz. Sizin de multi-Factor Authentication sunucusu kullanarak şirket içi uygulamalar ile birlikte kullanabilirsiniz.

**MFA senaryoları**

Oturum açma koruma banka oturum açmalar ve kaynak koduna erişim izinsiz girişi maliyeti yüksek finansal veya bir fikri özelliğine sahip olduğu gibi hassas hesapları.   

## <a name="mobile"></a>Cep telefonu
Bir mobil aygıt için bir uygulama oluşturuyorsanız, Azure veri hello bulutta depolamak, kullanıcıların kimliğini doğrulamak ve özel kod büyük bir bölümünü toowrite kalmadan anında iletme bildirimleri göndermek yardımcı olabilir.

Sanal makineler, bulut Hizmetleri veya Web uygulamaları kullanarak bir mobil uygulama için hello arka uç kesinlikle oluşturabilirsiniz, ancak daha az zaman yazma hello Azure Hizmetleri kullanarak hizmet bileşenlerinin temel harcayabilir.

### <a name="mobile-apps"></a>Mobile Apps
![Mobile Apps](./media/fundamentals-introduction-to-azure/MobileServicesIntroNew.png)

*Şekil: Mobil uygulamaları ile mobil cihazları arabirim uygulamaları tarafından genellikle gerekli işlevselliği sağlar.*

Azure mobil uygulamalar, bir mobil uygulama için bir arka uç oluştururken kaydedebileceğiniz pek çok yararlı işlevleri zaman sağlar. Toodo basit sağlama ve yönetim bir SQL veritabanında depolanan verilerin sağlar. Sunucu tarafı kodu ile kolayca blob depolama veya MongoDB gibi ek veri depolama seçeneklerini kullanabilirsiniz. Bazı durumlarda, bunun yerine bildirim hub'ları sonraki bölümde açıklandığı gibi kullanabilmenize rağmen Mobile Apps bildirimleri için destek sağlar.  Merhaba hizmet bir REST API de vardır ve mobil uygulamanıza tooget işlerini çağırabilirsiniz. Mobile Apps, ayrıca Microsoft ve Active Directory üzerinden tooauthenticate kullanıcıların yanı sıra diğer iyi bilinen kimlik sağlayıcıları Facebook, Twitter ve Google gibi hello yeteneği sağlar.   

Hizmet veri yolu ve çalışan rolleri gibi diğer Azure hizmetlerini kullanmak ve tooon içi sistemleri bağlanın. Hello Azure deposu (ör. SendGrid e-posta için) tooprovide ek işlevsellik gelen 3 taraf eklentilerin bile kullanabilir.

Yerel istemci kitaplıkları Android, iOS, HTML/JavaScript, Windows Phone ve Windows mağazası uygulamaları için daha kolay toodevelop tüm önde gelen mobil platformlarda olun. Mobile Services veri toouse ve farklı platformlarda uygulamalar ile kimlik doğrulaması işlevselliğini bir REST API sağlar. Cihazlar arasında tutarlı bir kullanıcı deneyimi sağlayabilmesi için tek bir mobil hizmette birden çok istemci uygulamaları yedekleyebilirsiniz.

Azure yüksek ölçüde ölçeklendirmeyi zaten desteklediğinden, uygulamanızı daha popüler hale geldiğinde hello trafiği işleyebilir.  İzleme ve günlüğe kaydetme desteklenir toohelp sorunlarını gidermek ve performans yönetin.

### <a name="notification-hubs"></a>Notification Hubs
![NotificationHubs](./media/fundamentals-introduction-to-azure/NotificationHubsIntroNew.png)  

*Şekil: Bildirim hub'ları ile mobil cihazları arabirim uygulamaları tarafından genellikle gerekli işlevselliği sağlar.*

Azure Mobile Apps'de toodo bildirimleri kod yazabilirsiniz olsa da, bildirim hub'ları dakika içinde en iyi duruma getirilmiş toobroadcast milyonlarca yüksek oranda kişiselleştirilmiş anında iletme bildirimleri durumdur.  Mobil taşıyıcı veya aygıt üreticisi gibi ayrıntıları hakkında tooworry yok. Tek tek veya kullanıcılar tek bir API çağrısı ile milyonlarca hedefleyebilirsiniz.

Bildirim hub'ları tüm arka ucu ile tasarlanmış toowork olur. Azure Mobile Apps, özel bir arka uç üzerinde herhangi bir sağlayıcıyı çalıştıran hello bulutta veya şirket içi arka uç kullanabilirsiniz.

**Bildirim hub'ı senaryoları** burada oynatıcıları sürdü kapatır mobil oyun yazıyorsanız toonotify player 2 gerekebilir, player 1 kendi bırakma tamamlandı. Bu tüm toodo ihtiyacınız olursa, yalnızca Mobile Apps kullanabilirsiniz. Ancak, 100.000 kullanıcı varsa, oyun ve hassas ücretsiz teklif tooeveryone, bildirim hub'ları hello daha iyi bir seçimdir birer toosend istiyorsunuz.

Düşük gecikme süresine sahip olayları ve ürün duyuru bildirimleri toomillions kullanıcıların sporting son dakika haberleri gönderebilirsiniz. Çalışanların e-posta veya diğer uygulamalar toostay haberdar denetleyin tooconstantly aktarıp kuruluşların çalışanlarına satış fırsatları gibi yeni saat hassas iletişimlerle ilgili bildirebilir. Bir-zamanlı çok faktörlü kimlik doğrulaması için gerekli parolaları da gönderebilirsiniz.

## <a name="back-up"></a>Yedekleme
Her Kuruluş toobackup ve geri yükleme veri gerekir. Azure toobackup ve uygulamanızı hello Bulut veya şirket içi geri yükleme kullanabilirsiniz. Azure yedekleme hello türüne bağlı olarak farklı seçenekler toohelp sunar.

### <a name="site-recovery"></a>Site Recovery
Azure Site Recovery (önceki adıyla Hyper-V kurtarma Yöneticisi) hello çoğaltma ve kurtarma siteleri arasında iletişime geçerek önemli uygulamaların korunmasına yardımcı olabilir. Site Recovery yetenek tooprotect uygulamalar Hyper-v, VMWare veya SAN tooyour kendi ikincil site, tooa barındırıcının site veya tooAzure göre ve hello gider ve derleme ve ikincil konumunuz yönetme karmaşıklığını önlemek sağlar. Azure verileri şifreler ve iletişimleri ve çok çalışmıyorken veri şifrelemeyi etkinleştirmek hello seçeneğiniz vardır.

Hizmetlerinizin hello durumunu kesintisiz olarak izler ve yardımcı hello düzenli bir site kesinti hello birincil veri merkezinde hello olayı Hizmetleri'nde kurtarılması otomatikleştirin. Sanal makineler bağımsızlıklar şekilde toohelp geri yükleme hizmetinde hızlı bir şekilde, daha karmaşık çok katmanlı iş yükleri için getirilebilir.

Site Recovery, Hyper-V çoğaltma, System Center ve SQL Server Always On gibi mevcut teknolojiler ile çalışır. Kullanıma [Azure Site Recovery genel bakış](site-recovery/site-recovery-overview.md) daha fazla ayrıntı için.

### <a name="azure-backup"></a>Azure Backup
![Azure Backup](./media/fundamentals-introduction-to-azure/AzureBackupIntroNew.png)  

*Şekil: Azure yedekleme verileri şirket içi Windows sunucularından hello bulutunu yedekler.*  

Azure yedekleme hello bulutunu Windows Server çalıştıran şirket içi sunuculardan verileri yedekler. Windows Server 2012, Windows Server 2012 Essentials veya System Center 2012 - Data Protection Manager yedekleme araçları hello doğrudan Yedeklemelerinizin yönetebilirsiniz. Alternatif olarak, özelleştirilmiş bir yedekleme aracısı kullanabilirsiniz.

Veriler Aktarımdan önce yedekler şifrelendiği daha güvenli ve şifrelenmiş olarak Azure depolanır ve karşıya yüklediğiniz bir sertifika tarafından korunan. Merhaba hizmeti aynı yedekli ve yüksek oranda kullanılabilir veri koruması Azure depolama alanında bulunan hello kullanır.  Tam veya artımlı yedeklemeleri dosyaları ve klasörleri düzenli bir zamanlamaya göre veya hemen yedekleyebilirsiniz. Toohello bulut yedeklenen verileri sonra yetkili kullanıcıların yedeklemeleri tooany sunucu kolayca kurtarabilirsiniz. Merhaba maliyet toostore ve Aktarım verileri yönetilebilir yapılandırılabilir veri bekletme ilkeleri, veri sıkıştırma ve veri azaltma aktarım sunar.

**Azure yedekleme için senaryolar**

Windows Server veya System Center zaten kullanıyorsanız, Azure yedekleme sunucuları dosya sistemi, sanal makineler ve SQL Server veritabanlarını yedeklemek için doğal bir çözüm varsa.  Şifrelenmiş, seyrek ve sıkıştırılmış dosyaları ile çalışır. Bazı sınırlamalar vardır, size gereken şekilde [hello Azure Backup önkoşulları denetleyin](http://technet.microsoft.com/library/dn296608.aspx) ilk.

## <a name="messaging-and-integration"></a>Mesajlaşma ve Tümleştirme
Ne yapmakta olduğu olsun, kod toointeract diğer kod ile sık gerekir.  Bazı durumlarda, gereken tek şey temel kuyruğa alınan Mesajlaşma. Diğer durumlarda, daha karmaşık etkileşimler gereklidir. Azure, bu sorunları birkaç farklı şekilde toosolve sağlar. Şekil 5 hello seçenekler gösterilmektedir.

### <a name="queues"></a>Kuyruklar
![Azure Service Bus geçişi](./media/fundamentals-introduction-to-azure/QueuesIntroNew.png)

*Şekil: Sıraları uygulama bölümleri arasında Kuplaj gevşek izin ve ölçeklendirme kolaylaştırabilirsiniz.*  

Queuing olan basit bir fikir: bir uygulama bir ileti sıraya koyar ve bu iletiyi sonunda başka bir uygulama tarafından okunur. Uygulamanızı basit bu hizmet gerekiyorsa, Azure kuyrukları hello en iyi seçim olabilir.

Zaman içinde Azure büyüdü hello şekilde hello nedeniyle, Azure depolama kuyruklar ve hizmet veri yolu kuyrukları benzer sıraya alma hizmetleri sağlar. neden istediğiniz hello üzerinden toouse diğer hello nedenleri hello oldukça teknik yazıda ele alınmıştır [Azure kuyruklar ve hizmet veri yolu kuyrukları karşılaştırılan ve Contrasted -](http://msdn.microsoft.com/library/azure/hh767287.aspx).  Birçok senaryoda ya da çalışır.

**Sıra senaryoları**

Bir genel sıraların Bugün bir web rolü örneği içinde çalışan rol örneği ile iletişim kurabilir toolet kullanılmasıdır aynı bulut Hizmetleri uygulama hello.

Örneğin, video paylaşımı için bir Azure uygulaması oluşturduğunuzu varsayalım. Merhaba uygulaması kullanıcıların karşıya yükleme ve C çeviren # öğesinde uygulanan bir çalışan rolü ile birlikte video izlemesine olanak tanır karşıya bir web rolünde çeşitli biçimlere video çalışan PHP kodunun oluşur.

Bir web rolü örneği bir kullanıcıdan yeni bir video aldığında bir blob'a hello video depolamak, ardından bunu belirten bir kuyruk aracılığıyla ileti tooa çalışan rolü Gönder nerede toofind bu yeni video. Bir çalışan rolü örneği BT hello sıradan bir sonra okuma hello ileti önemli ve gerekli hello video çevirileri hello arka planda gerçekleştirmek değil.

Bir uygulama bu şekilde yapılandırılması zaman uyumsuz işleme sağlar ve ayrıca hello sayısı web rolü örnekleri ve çalışan rolü örnekleri bağımsız olarak değiştirilebilir bu yana uygulama daha kolay tooscale hello kolaylaştırır. Çalışan rollerini yukarı ve aşağı tetikleyici tooscale hello sayısı olarak hello sıra boyutu de kullanabilirsiniz. Çok yüksek ve daha fazla rolü ekleyin. Alt aldığında toosave para rolleri çalıştıran hello sayısını azaltabilir.  

Web ve çalışan rolleri kullanmasanız bile, uygulamanızın birçok farklı bölümleri arasında aynı bu deseni kullanabilirsiniz.  Yukarı ve aşağı hello sırası isteğe bağlı olarak her iki tarafında tooscale hello bölümleri sağlar ve işleme süresi gerektirir.

### <a name="service-bus"></a>Service Bus
Bir mobil cihaz veya başka bir yere, veri merkezinizdeki hello bulutta çalıştırdıkları olup olmadığını uygulamaları toointeract gerekir. Hello Azure Service Bus, neredeyse her yerden çalışan toolet uygulamaların veri değişimi hedeftir.

Daha önce açıklanan ek toohello kuyruklarda (birebir), hizmet veri yolu tooother de iletişim yöntemleri sağlar.

#### <a name="service-bus-relay"></a>Service Bus Geçişi
![Azure Service Bus geçişi](./media/fundamentals-introduction-to-azure/ServiceBusRelayIntroNew.png)

*Şekil: Service Bus geçişi bir Güvenlik Duvarı'nın farklı yüze uygulamalar arasında iletişim sağlar.*

Hizmet veri yolu, güvenlik duvarları üzerinden güvenli şekilde toointeract sağlayan kendi geçiş hizmeti üzerinden doğrudan iletişim sağlar. Service Bus geçişlerini hello bulutta yerine yerel olarak barındırılan bir uç nokta aracılığıyla iletileri değiş tokuş ederek uygulamaları toocommunicate etkinleştirin.

**Service Bus geçiş senaryoları**

Service Bus ile iletişim kurmak uygulamaları Azure uygulamalarını veya bazı başka bulut platformunda çalışan yazılımı olabilir. Bunlar ayrıca hello bulut dışında ancak çalışan uygulamalar olabilir. Örneğin, kendi veri merkezi içinde bilgisayarlarda ayırma Hizmetleri uygulayan bir uçak düşünün. Merhaba uçak tooexpose check-in kiosk havaalanları, ayırma Aracısı Terminal ve hatta belki de müşterilerin telefonları dahil olmak üzere bu hizmetleri toomany istemciler gerekir. Bu hizmet veri yolu toodo bu hello arasında kabaca eşleşmiş etkileşimler çeşitli uygulamaları oluşturma kullanabilir.

#### <a name="service-bus-topics-and-subscriptions"></a>Hizmet Veri Yolu Konuları ve Abonelikleri
![Azure Service Bus konuları](./media/fundamentals-introduction-to-azure/ServiceBusTopicsSubsIntroNew.png)   
 *Şekil: Service Bus konuları, birden çok uygulamaları toopost iletileri ve belirli bir ölçüte uyan diğer uygulamaları toosubscribe tooreceive iletileri sağlar.*

Service Bus konuları ve abonelikleri adlı Yayımla ve abone ol bir mekanizma sağlar. Diğer uygulamalar abonelikleri toothis konu oluşturabilirsiniz, ancak publish-subscribe ile iletileri tooa konu, bir uygulama gönderebilirsiniz. Bu uygulamalar, aynı iletiyi birden çok alıcılar tarafından okunabilmesini olması hello izin vererek kümesi arasında bir çok iletişimi sağlar.

**Service Bus konuları ve abonelikleri senaryoları**

Burada tüm önemli birçok iletileri vardır, ancak çeşitli aşağı akış sistemleri bu iletişimi toolisten toodiffering kümelerine yeterlidir ayarladığınız zaman, hizmet veri yolu konusu ve abonelikleri iyi bir seçenek olan.

### <a name="biztalk-services"></a>BizTalk Services
![BizTalk Hizmetleri](./media/fundamentals-introduction-to-azure/BizTalkServicesIntroNew.png)   
 *Şekil: BizTalk Services hello özelliği tootransform XML iletileri biçimleri hello bulutta sağlar.*

Bazen farklı ileti biçimi kullanarak iletişim sistemlerini bağlamak. İş toohave farklı veritabanı şemaları ve XML biçimleri, ortak bir standart kullanılabilir olduğunda bile messaging için yaygın bir durumdur. Çok fazla özel kod yazmak yerine, BizTalk Server şirket içi toointegrate çeşitli sistemleri kullanabilirsiniz.  Azure BizTalk Services sağlar hello hizmetinin ancak hello bulutta aynı türde. Yalnızca ne kullanın ve tooon içi olurdu gibi ölçek hakkında endişelenmeyin için ödeme.

**Senaryoları BizTalk Hizmetleri**

İşletmeden işletmeye (B2B) etkileşimleri çeviri bu tür sık gerektirir.  Örneğin, Uçaklar gereksinimlerini tooorder parçalarını oluşturma bir çeşitli bölümlerini üreticiler bir şirkettir. Birçok bölümleri sağlayıcıdan sahip olur.  Bu sipariş doğrudan sistemlerden hello uçak oluşturucular hello Üreticiler sistemleri içine otomatik toogo olmalıdır.  Çekirdek sistemlerini ve ileti formatları hiçbiri iş toochange istediği ve bu biçimleri olan Merhaba, aynı çok olası değil. BizTalk Services iletiler alabilir ve hello yeni biçimleri her iki yönde arasında çevir. Her iki hello uçak tedarikçi iş tootranslate hello veya çeşitli üreticiler hello gerekli çevirisi, daha fazla denetim ve hello miktarını isteyen bağlı olabilir.     

## <a name="compute-assistance"></a>Yardım işlem
Azure toorun tüm hello saat gerekmez Hizmetleri için desteği sağlar.  

### <a name="scheduler"></a>Scheduler
![Azure Scheduler](./media/fundamentals-introduction-to-azure/SchedulerIntroNew.png)   
*Şekil: Azure Zamanlayıcı belirli bir süre için belirli bir zamanda işleri şekilde tooschedule sağlar.*

Bazen uygulamalar yalnızca belirli bir süre sonunda toorun gerekir. Azure üzerinde bu tür bir uygulama için veri tooprocess bekleyen 24 x 7 yalnızca çalışmaya devam izin vererek yerine uygulama paradan tasarruf edebilirsiniz. Bir uygulama süresi veya bir takvim aralığına göre çalıştırılması gereken zaman azure Zamanlayıcı tooschedule sağlar. Güvenilir ve ağ, makine ve veri merkezi hataları olsa bile bir işlemin çalıştığını doğrulayın. Bu eylemler hello Scheduler REST API toomanage kullanın.

Zamanlanmış bir uyarı oluştuğunda, Zamanlayıcı HTTP veya HTTPS iletileri tooa belirli uç gönderir veya bir ileti bir depolama kuyruğu koyabilirsiniz.  Toohave gerekir böylece uygulamanız erişilebilir bir uç nokta içerecek veya sahip bir depolama kuyruğu izleme. Merhaba iletisini alır sonra için programlanmış hangi eylemini gerçekleştirebilirsiniz.

**Zamanlayıcı senaryoları**

* Yinelenen uygulama eylemleri: örnek olarak, bir hizmet düzenli aralıklarla veri twitter'dan almak ve normal akışa hello verileri toplayın.
* Günlük Bakım: günlük işleme veya temizleme, yedekleme gerçekleştirme ve diğer aralıklı görev zamanlama.
* Gece çalıştırmak görevler.
* Web uygulamaları görevleri günlük ayıklanması, yedeklemelerin ve diğer bakım görevlerini gerçekleştirme günlükleri, ister. Bir yönetici toobackup kendi veritabanı hello için her gün 1 sabah sonraki 9 ay içerisinde, örneğin seçebilirsiniz.

Merhaba Scheduler API'si toocreate sağlar, güncelleştirme, silme, görüntülemek ve iş koleksiyonları ve zamanlanmış işler programlı olarak yönetmek.

## <a name="performance"></a>Performans
Performans her zaman bir uygulama için önemlidir. Uygulamaları eğilimindedir tooaccess aynı verileri tekrar tekrar hello. Tek yönlü tooimprove performans tookeep bu verileri daha yakından toohello uygulaması bir kopyasını, başlangıç zamanı en aza gerekli tooretrieve onu. Azure Bunu yapmak için farklı hizmetler sağlar.

### <a name="azure-caching"></a>Azure Önbelleği
![Azure Önbelleği](./media/fundamentals-introduction-to-azure/AzureCacheIntroNew.png)   
 **Şekil: Bir Azure uygulama verilerini bellekte önbelleğe ve hatta çok sayıda çalışan rolleri arasında bölmek**

Azure'nın veri yönetimi hizmetlerini SQL Database, tablolar veya BLOB hiçbirinde depolanan verilere-oldukça hızlıdır. Henüz bellekte depolanan verilere erişme daha hızlıdır. Bu nedenle, bir bellek içi kopya sık erişilen veri tutma uygulama performansını iyileştirebilir. Azure'nın bellek içi önbelleğe alma toodo bunu kullanabilirsiniz.

Bulut Hizmetleri uygulama verileri bu önbellekte depolamak sonra tooaccess kalıcı depolama gerek kalmadan doğrudan almak. Merhaba önbellek uygulamanızı VMs kullanıcının ya da VM'ler tarafından sağlanan iç yalnızca toocaching ayrılmış korunabilir. Her iki durumda da hello önbellek dağıtılabilir, hello verilerle bir Azure veri merkezinde birden çok VM üzerinden yayılan içeriyor.

Azure zamanla gölgeye farklı önbellek teknolojileri sayısına sahip. Bunlar sunuldu hello sırayla yoktur paylaşılan, rol yönetilen ve Redis önbelleği. Merhaba paylaşılan önbelleğe alma eski bir teknolojidir ve yeni uygulamalar ile oluşturmamalısınız. Merhaba yönetilen önbellek rol hello aynı özelliklerini önbelleğe ancak dışında yönetilen hizmet olarak Azure Yönetim Portalı hello hello sahiptir. Merhaba Redis önbelleği önizlemede değil. Merhaba Redis uygulama özelliklerinin hello en büyük sayı olan ve yeni önbelleğe alma kodu yazarken önerilir.

**Azure önbelleği senaryoları**

Bir ürün kataloğu art arda okuyan bir uygulama önbelleğe alma bu tür kullanmanın avantajları, örneğin, bu yana hello verileri daha hızlı kullanılabilir olması. Merhaba teknolojisi, kilitleme, salt okunur verileri yanı sıra okuma/yazma ile kullanıldığını izin vererek de destekler. Ve ASP.NET uygulamaları yalnızca bir yapılandırma değişikliği hello hizmet toostore oturum verilerini kullanabilirsiniz.

### <a name="content-delivery-network"></a>Content Delivery Network
![Azure CDN](./media/fundamentals-introduction-to-azure/CDNIntroNew.png)   
 **Şekil: Merhaba Dünya sitelerdeki blob kopyaları önbelleğe alınabilir.**

Merhaba Dünya kullanıcılar tarafından erişileceği toostore blob verilerini gerektiğini varsayalım. Belki de bir video hello son World fincanı eşleşme, örneğin, sürücü güncelleştirmesi veya popüler bir e-kitap olur. Birden çok Azure veri merkezlerinde hello verilerin bir kopyasını saklamak yardımcı olur, ancak çok sayıda kullanıcı varsa, bu yeterli muhtemelen gerekmez. Daha iyi performans için hello Azure CDN kullanabilirsiniz.

Merhaba CDN siteleri düzinelerce Merhaba dünya genelinde kopyalarını Azure BLOB Depolama her özellikli sahiptir. Merhaba ilk kez kullanıcı Merhaba Dünya bazı parçası olarak belirli bir blob eriştiğinde içerdiği hello bilgileri Azure veri merkezinden bu Coğrafya yerel CDN depolama kopyalanır. Bundan sonra erişimleri bu bölümünden hello World hello CDN önbelleğe hello blob kopyalama kullanacağı-Azure veri merkezinde en yakın tüm hello yolu toohello toogo gerekmez. Merhaba, daha hızlı erişim erişilen toofrequently veri Merhaba Dünya başka bir yerindeki kullanıcılar tarafından sonucudur.

**CDN senaryoları**

Ortak toouse CDN, dünya çapında Media Services toodeliver video olur. Video genellikle büyük ve çok miktarda bant genişliği gerektirir.  Media Services hakkında başka bir yerde bu sayfada açıklandı.

## <a name="big-data-and-big-compute"></a>Büyük veri ve Big Compute
### <a name="hdinsight-hadoop"></a>HDInsight (Hadoop)
![Hdınsight](./media/fundamentals-introduction-to-azure/HDInsightIntroNew.png)   
 **Şekil: Hdınsight, büyük miktarlarda veri toplu işleme hello yardımcı olur.**

Birçok yıldır hello toplu veri analizi ilişkisel DBMS ile oluşturulmuş bir veri ambarına depolanan ilişkisel veri üzerinde gerçekleştirilmedi. Bu tür bir İş analizi hala çok önemlidir ve uzun süre toocome için olacaktır. Ancak ne tooanalyze istediğiniz hello verileri ilişkisel veritabanları yalnızca işleyemiyor kadar büyük değil mi? Ve hello veri ilişkisel olmayan varsayalım? Bir veri merkezinde, örneğin, veya algılayıcılar geçmiş olay verilerden veya başka bir olay günlüklerini olabilir. Bu gibi durumlarda, büyük veri sorun olarak bilinir vardır. Başka bir yaklaşım gerekir.

büyük veri çözümleme için bugün hello baskın Hadoop teknolojisidir. Apache kaynak projeyi açın, bu teknoloji hello Hadoop dağıtılmış dosya sistemi (HDFS) kullanarak verileri depolar, sonra bu verileri MapReduce işleri tooanalyze oluşturmalarını sağlar. HDFS veri hello MapReduce işi hello büyük veri izin vererek, her birinde çalışır parçalarını paralel olarak işlenmesi sonra birden çok sunucu arasında yayar.

Hdınsight hello hello Azure'nın Apache Hadoop tabanlı hizmetin adıdır. Hdınsight hello kümede verileri depolamak ve arasında birden çok VM dağıtmak HDFS olanak sağlar. Ayrıca bir MapReduce işi hello mantığını bu VM'ler arasında yayar. Yalnızca şirket içi Hadoop ile veri işlenen yerel olarak-hello mantığı ve üzerinde çalıştığı hello veri olarak olarak aynı VM hello- ve daha iyi performans için paralel. Hdınsight, ayrıca Azure depolama kasası (BLOB'ları kullanan ASV içinde), veri depolayabilirsiniz.  ASV kullanarak Hdınsight kümenize kullanılmadığında silin, ancak hala hello bulutta verilerinizi korumak için toosave para da sağlar.

Hdınsight Hive veya Pig dahil olmak üzere diğer bileşenleri hello Hadoop ekosistemi de destekler. Microsoft ayrıca, daha kolay toowork Hdınsight tarafından üretilen verilerle hello HiveODBC bağdaştırıcısı ve Excel ile iş Veri Gezgini gibi geleneksel BI araçları kullanarak bileşen oluşturmuştur.

### <a name="high-performance-computing-big-compute"></a>Yüksek performanslı bilgi işlem (Big Compute)
Merhaba en cazip yolları toouse bir bulut platformu toorun yüksek performanslı bilgi işlem (HPC) ve diğer "Big Compute" uygulamalardan biridir. Örnekler özel mühendislik oluşturulan uygulamaların toouse endüstri standardı ileti geçirme arabirimi (MPI) gibi sözde utandırıcı derecede paralel uygulamalar, bu tür finansal risk modelleri hello.

Big Compute Hello özünü Yürütülüyor kod hello en çok sayıda makinelerde aynı anda. Azure üzerinde bu çok sayıda sanal makineyi aynı anda çalışan tüm paralel toosolve bazı sorun çalışma anlamına gelir. Bunun yapılması bazı yolu tooresources ve tooschedule uygulamalar, yani, toodistribute Bu örneklerde, iş gerektirir. Microsoft'un ücretsiz HPC Pack ve diğer bilgi işlem küme çözümleri de Azure, yararlanarak tooadd kapasite isteğe bağlı tooan işlem kümesi veya tamamen hello Big Compute uygulamalarını çalıştıran şirket içi Azure hesaplama ve altyapı hizmetleri gerçekleştirebilirsiniz bulut.

Azure, bir aralık VM örneği boyutlarının CPU çekirdekleri, bellek, disk kapasitesi ve diğer özellikleri toomeet hello gereksinimleri farklı uygulamalar farklı yapılandırmalarıyla sağlar. Hello yakın zamanda sunulan A8 ve A9 örnekleri iş için birçok işlem yoğun iş yükleri ve paralel MPI uygulamaları özellikle, yüksek hız, çok çekirdekli CPU ve büyük miktarlarda bellek sahip oldukları için. Belirli yapılandırmalarında hello örnekleri düşük gecikme süreli ve yüksek işleme uygulama ağı en yüksek verimlilik paralel MPI uygulamaları için doğrudan uzak bellek erişimi (RDMA) teknolojisini içeren hello bulutta yararlanın.

Azure Big Compute uygulama geliştiricileri ve iş ortakları ayrıca bir kümesini hesaplama özellikleri, hizmetler, mimari seçim ve geliştirme araçları sunar. Azure özel veri iş akışları içeren özel Big Compute iş akışları destekler ve iş ve görev toothousands, ölçeklenebilir desen zamanlama çekirdek işlem.

## <a name="media"></a>Medya
![Azure medya Hizmetleri](./media/fundamentals-introduction-to-azure/MediaServicesIntroNew.png)   
 **Şekil: Media Services, video ve diğer medya tooclients Merhaba Dünya sağlayan uygulamalar için bir platformdur.**

Video Internet trafiğini büyük bir bölümünü bugün yapar ve söz konusu yüzdesi yarın daha da büyük olacaktır. Henüz video hello Web'de sağlayan basit değil. Değişkenleri çok sayıda vardır, hello kullanıcının ekran çözünürlüğü gibi hello şifreleme algoritmasını ve hello gösterme. Video da toohave WINS'e gibi pek çok kişiyle toowatch çevrimiçi film istediğiniz karar verdiğinizde bir Cumartesi gece ani talep eğilimlidir.

Kendi popülerliği verildiğinde, birçok yeni uygulama kullanım videonun oluşturulacak sonuç güvenli değil. Bunların tümünün toosolve bazı gerekir henüz Merhaba aynı sorunları ve her biri kendi başına bu sorunları çözmek hale anlamlı yok. Toocreate yaygın çözümleri için birçok uygulamaları toouse sağlayan bir platform buna daha iyi bir yaklaşımdır. Ve bu platformu hello bulutta oluşturma Temizle bazı avantajları vardır. Kullandıkça Öde temelinde geniş çapta kullanılabilir olabilir ve ekran uygulamaları genellikle yüz talep hello değişkenlik işleyebilir.

Azure Media Services, bu sorunu giderir. Yaşam oluşturma ve video ve diğer medya kullanarak uygulamaları çalıştırma kişiler için daha kolay hale getirmek bulut bileşenleri kümesi sağlar.

Merhaba şekil gösterildiği gibi Media Services, video ve diğer medya ile çalışan uygulamalar için bir bileşen kümesi sağlar. Örneğin, bir ortam içerir (Bu depolandığı Azure BLOB'ları) Media Services, çeşitli video ve ses biçimlerini destekleyen bir kodlama bileşeni, dijital hak yönetimi sağlayan bir içerik koruma bileşeni bileşen tooupload video alma Reklam video akışı, akış bileşenleri ve daha fazlasını ekleme ile ilgili bir bileşendir. Microsoft iş ortaklarını da hello platformu için bileşenleri sağlayın, sonra bu bileşenleri dağıtma ve onların adına faturalandırmak Microsoft sahip.

Bu platform kullanan uygulamaları Azure veya başka bir yerde çalıştırabilirsiniz. Örneğin, bir masaüstü uygulaması bir video üretim ev video tooMedia Hizmetleri karşıya kullanıcılarına sağlayabilir için daha sonra işlemek, çeşitli yollarla. Alternatif olarak, Azure üzerinde çalışan bir bulut tabanlı içerik yönetim hizmeti bir Media Services tooprocess üzerinde kullanır ve video dağıtın. Yerde çalışır ve bunu yapar, hangi bileşenlerin her uygulama seçer RESTful arabirimleri aracılığıyla erişme toouse gerekiyor.

toodistribute ne oluşturur, yalnızca gönderme BITS doğrudan toousers veya, bir uygulama hello Azure CDN, başka bir CDN kullanabilirsiniz. Ancak, var. alır, görüntü Media Services'i kullanarak oluşturulan Windows, Macintosh, HTML 5, iOS, Android, Windows Phone, Flash ve Silverlight dahil olmak üzere çeşitli istemci sistemleri tarafından kullanılabilecek. Merhaba hedeftir toomake bunu daha kolay toocreate modern medya uygulamaları.

**Başvuruları**

Media Services nasıl çalıştığını daha görsel görünümünü için hello karşıdan [Azure Media Services posteri][Azure Media Services Poster].

## <a name="commerce"></a>Ticaret
Merhaba neden bir hizmet olarak yazılım uygulamaları nasıl oluşturuyoruz dönüştürme. Bu ayrıca nasıl biz uygulamaları satmak dönüştürme. Bir SaaS uygulaması hello bulutta yaşadığı olduğundan, olası müşterilerine çevrimiçi çözümleri görünmelidir anlamlı olur. Ve bu değişiklik tooapplications yanı sıra toodata uygular. Neden kişiler toohello bulut piyasada veri kümeleri için görünüyor döndürmemelidir? Microsoft bu sorunları hello ile her ikisi de adresleri [Azure Marketi](https://azure.microsoft.com/marketplace/).

![Azure ticaret](./media/fundamentals-introduction-to-azure/CommerceIntroNew.png)   
 **Şekil: Azure Market ve Azure depolama bulmanıza ve Azure uygulamalarını ve ticari veri kümeleri satın alın ve bunları Azure uygulamalarınızı bir parçası olarak kullanın olanak tanır.**

Merhaba hello iki arasındaki farkı Market hello Azure Yönetim Portalı dışında olan, ancak hello depolama alanından erişilebilir olan hello portalın içinde. Potansiyel müşterilerle toofind Azure arama ihtiyaçlarına uygulamalar. Müşteriler, demografik veriler, finansal verileri, coğrafi veriler ve benzeri ticari veri kümeleri için de arayabilirsiniz. Bunlar şey istedikleri bulduğunuzda, bunlar, hello satıcıdan ya da doğrudan hello Market ya da depolama web konumlarına yoluyla veya bazı durumlarda hello Yönetim Portalı'ndan erişebilirsiniz. Uygulamaları hello Bing arama API hello erişim toohello web arama sonuçlarını vermiş Market üzerinden de kullanabilirsiniz.

**Ticaret senaryoları**

SendGrid hello toosend e-posta sağlayan Azure depolama bir uygulamadır. Güvenilir teslim ve istatistikler gibi ek işlevsellik sağlar.  Bu uygulama ve ilgili hizmetleri satın yerine, toobuild böyle bir altyapı kendiniz deneyin.  

## <a name="getting-started"></a>Başlarken
Merhaba büyük-resim, hello sonraki adıma sahip olduğunuza toowrite ilk Azure uygulamanızı ' dir. Dilinizi seçin [alma uygun SDK hello](/downloads/)ve bunun için gidin. Bulut bilgi işlem varsayılandır hello yeni--hemen kullanmaya başlayın.

[Azure Media Services Poster]: http://azure.microsoft.com/documentation/infographics/media-services/
