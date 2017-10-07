---
title: "aaaApproach ve işlem için Azure veri Kataloğu'nu benimseme | Microsoft Docs"
description: "Bu makale, Azure Veri Kataloğu'nu benimsemeyi planlayan kuruluşlar için, vizyon tanımlama, işle ilgili önemli kullanım durumlarını belirleme ve pilot proje seçme aşamaları da dahil olmak üzere bir yaklaşım ve süreç sağlamaktadır."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 0c771e7a-6fcd-417f-9247-897177719567
ms.service: data-catalog
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 06/15/2017
ms.author: maroche
ms.openlocfilehash: ffa6993b63c8a6066f48727fb046d0334a6df541
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="approach-and-process-for-adopting-azure-data-catalog"></a>Azure Veri Kataloğu'nu benimseme yaklaşımı ve işlemi
Bu makale, kuruluşunuzda **Azure Veri Kataloğu**'nu benimsemeye başlamanıza yardımcı olacaktır. toosuccessfully benimsemeyi **Azure veri Kataloğu**, üç temel öğeye odaklanmayı: VİZYONUNUZU tanımlama, kuruluşunuz içindeki önemli iş kullanımı durumlarını tanımlamak ve pilot proje seçme.

## <a name="introducing-hello-azure-data-catalog"></a>Hello Azure veri Kataloğu giriş
İçinde Merhaba Dünya çalışmanın nasıl veri varlıkları hakkında uzman bilgilerine mümkün toofind olmalıdır, kişilerin beklentilerini değişti. Bugün, iş yerinde yaygın kullanımı hello Yammer gibi sosyal medya araçlarının ile kişilerin toobe mümkün tooquickly get Yardım ve öneri çeşitli konularda üzerinde bekler. **Azure Veri Kataloğu**, işletmelerin ve ekiplerin kurumsal veri varlıklarıyla ilgili bilgileri merkezi bir depoda bir araya getirmesine yardımcı olur. Veri tüketicileri, bu veri varlıklarını bulabilir ve konu uzmanlarının sunduğu bilgileri edinebilir.

Bu makalede kullanmaya bir yaklaşım toogetting sunar **Azure veri Kataloğu**. Merhaba makalede, Adventure Works adlı kurgusal şirket hello için tipik bir veri Kataloğu benimseme planı açıklanmaktadır.

**Azure Veri Kataloğu nedir?**

**Azure Veri Kataloğu**, Azure'da bulunan tam yönetimli bir hizmet olmasının yanı sıra self servis veri kaynağı bulmaya olanak tanıyan, kuruluş genelinde geçerli bir bilgi (meta veri) kataloğudur. Veri Kataloğu ile kaydetme, Bul, açıklama ve toodata varlıklar bağlanın. Veri Kataloğu bunları kolay toofind veri varlıklarını anlamasını ve toothem bağlanın tasarlanmış toomanage farklı bilgi varlıklarını toomake ' dir. Kullanılabilir verileri hello zaman toogain Öngörüler azaltır ve hello değeri tooorganizations artırır. toolearn daha, fazla [Microsoft Azure veri Kataloğu](https://azure.microsoft.com/services/data-catalog/).

## <a name="azure-data-catalog-adoption-plan"></a>Azure Veri Kataloğu benimseme planı
Bir **Azure veri Kataloğu** benimseme planı açıklanmaktadır nasıl hello hizmeti kullanmanın yararları hello iletildiğinden toostakeholders ve kullanıcıların ve ne tür, eğitim toousers sağlarlar. Bir anahtar başarı sürücü tooadopt veri Kataloğu hello değeri hello hizmet toousers ve Paydaşlar iletişim ne kadar etkin olur. Merhaba ilk benimseme planındaki birincil hedef kitle hello hizmetinin hello kullanıcılardır. Paydaşlardan ne Al ne kadar satınalma bileşenini olsun hello kullanıcıları veya müşterileri, veri Kataloğu hizmetinizin bu kullanımları dahil etmediği, hello benimseme başarılı olmaz. Bu nedenle, bu makalede paydaş desteğine sahip olduğunuz varsayılarak Veri Kataloğu'nun kullanıcılar tarafından benimsenmesine yönelik bir plan oluşturulmasına odaklanılmıştır.
Hangi veri Kataloğu ile mümkündür ve onlara verir kişiler hello bilgi ve yönergeler tooachieve etkili bir benimseme planı başarıyla prosese onu. Kullanıcıların kendi işlerinde başarılı toohelp veri Kataloğu sağlar toounderstand hello değer gerekir. Kişiler veri Kataloğu bunları verilerle daha fazla sonuç elde nasıl yardımcı olabileceğini gördüğünde, veri Kataloğu'nu benimsemenin hello değeri açıkça ortaya çıkar. Etkili bir planda tootake hello değişimin zorluklarının da hesaba gereken şekilde değişiklik zordur.

Benimseme planı, kişilerin toosucceed için kritik iletişim kurmak ve hedeflerine ulaşması yardımcı olur. Tipik bir planı nasıl veri Kataloğu toomake kullanıcıların yaşamlarını daha kolay geçiyor ve hello aşağıdaki bölümleri içerir açıklanmaktadır:

* **Vizyon mesajı** -hello benimseme planı, kullanıcılar ve Paydaşlar ile yönelik olarak kısaca ele yardımcı olur. Bu, kısa sunum fırsatınızdır.
* **Pilot ekip ve etkileyici** - bir pilot ekip ve etki sahipleri Yardım İyileştir nasıl toointroduce ekipleri ve kullanıcıların tooData katalog öğrenme. Etki sahipleri, diğer kullanıcılara akran koçluğu yapabilir. Ayrıca önündeki engelleri ve tooadoption belirlemenize yardımcı olur.
* **İletişim ve hareket planı** -kullanıcıların toounderstand yardımcı nasıl veri Kataloğu, yardımcı takımlar organik bir benimseme verildiğine ve sonuç olarak tüm kuruluş hello.
* **Eğitim planı** - genellikle müşteri adayları tooadoption başarılı olmasına ve olumlu sonuçlara eğitim kapsamlı.

Bazı ipuçları toodefine İşte bir **Azure veri Kataloğu** benimseme planı.

## <a name="define-your-data-catalog-project-vision"></a>Veri Kataloğu proje vizyonunuzu tanımlama
İlk adım toodefine hello bir **Azure veri Kataloğu** benimseme planı olan toowrite ne çalıştığınız bir ilgi uyandırıcı açıklaması tooaccomplish. En iyi tookeep hello görme deyimi mesajını geniş henüz yeterince kısa toodefine belirli kısa vadeli ve uzun vadeli hedefleri olur.

VİZYONUNUZU tanımlamanıza bazı ipuçları toohelp şunlardır:

* **Merhaba önemli dağıtım teşvikini tanımlama** -veri Kataloğu kullanılarak ele alınabilecek hello iş hello belirli veri kaynağı yönetim düşünmek gerekir. Size yardımcı olacak durum veri Kataloğu'nu kullanarak hello üst yararları. Örneğin, olabilir tüm yeni çalışanların toolearn hakkında ve kullanılması gereken genel veri kaynakları veya yalnızca birkaç anahtar kişinin ayrıntılı olarak kavraması gereken önemli ve karmaşık veri kaynakları. **Azure veri Kataloğu** bu veri kaynaklarını kolayca toodiscover yapın ve anlamak, böylece bu iyi bilinen bir sorun teşkil edecek noktalar doğrudan ve erken hello hizmet hello benimseme içinde çözülebilir yardımcı olabilir.
* **Kısa ve NET** - A Temizle hello görme anlayış alır herkes hello üzerinde aynı sayfa hello değeri veri Kataloğu hakkında toohello kuruluş ve hello görme kuruluş hedefleri nasıl destekler? sağlar.
* **Kişiler toowant toouse veri Kataloğu esin** - görme ve iletişim planınız kişilere, veri Kataloğu toofind yararlanabilir ve toodata kaynakları tooachieve verilerle daha fazla bağlantı terimleri toorecognize.
* **Hedefler ve zaman çizelgesi belirtin** - Bu, benimseme planınızın ayrıntılı ve erişilebilir sonuçlara sahip olmasını sağlar. Bir zaman çizelgesi herkesin odağını korur ve kontrol noktaları toomeasure başarı için sağlar.

Bir örnek Vizyon hello Adventure Works adlı kurgusal şirket için bir veri Kataloğu benimseme planı için şöyledir:

**Azure veri Kataloğu** hello Adventure Works Finans takım toocollaborate anahtar veri kaynaklarında güçlendirir, böylece her ekip üyesi, kolayca bulmak ve hello verileri kullanmak kendisinin gerekiyor ve kendi bilgi bir bütün olarak hello ekibi ile paylaşabilirsiniz.

Net bir vizyon mesajınız olduğunda, Veri Kataloğu için uygun bir pilot proje tanımlamanız gerekir. Genellikle, ilgili bazı ipuçları tooidentify durumlarda kullanan hello sonraki bölümde verilmektedir şekilde veri kataloğu için birkaç senaryo vardır.

## <a name="identify-data-catalog-business-use-cases"></a>Veri Kataloğu iş kullanım durumları tanımlama
ilgili tooData Kataloğu olan tooidentify kullanım örnekleri Göster çeşitli iş birimleri tooidentify ilgili kullanım durumlarını ve iş sorunlarını toosolve uzmanlarla. Kişilerin veri varlıklarını tanımlama ve anlama konusunda karşılaştığı mevcut sorunları gözden geçirin. Örneğin, ekipler veri varlıkları hakkında bilgileri yalnızca ilgili veri kaynaklarına sahip hello kuruluşunuzdaki birkaç kişiye danıştıktan sonra mı ediniyor?

Başarıya ulaşılacak durumlardır temsil en iyi toochoose kullanım örnekleri olan: durumlar, önemli oldukları veri Kataloğu ile çözülerek yüksek olasılık başarı henüz yok.

Tooidentify kullanım örnekleri bazı ipuçları şunlardır:

* **Merhaba ekibinin Hello hedeflerinizi** - mu hello takım elde nasıl hedeflerine? Bu aşamada toobe hedefi istediğinden veri Kataloğu odaklanmak henüz yok. Merhaba teknolojisi hakkında değil hello iş sonuçlarıyla ilgili olduğunu unutmayın.
* **Merhaba iş sorununu tanımlayın** -bulma ve veri varlıkları hakkında bilgileri öğrenme ilgili hello ekibi tarafından karşılaştığı hello sorunlar nelerdir? Örneğin, önemli veri kaynakları hakkında bilgi bir ağ klasöründeki Excel çalışma kitaplarında bulunabilir ve hello takım hello çalışma kitaplarını bulmak çok zaman harcayabilir.
* **Takım kültür ilgili toochange anlamak** -birçok benimseme zorluğu tooresistance toochange ilişkili yerine yeni bir aracı uyarlamasını hello. Kullanım tanımlarken toochange önemli bir takım nasıl yanıt vereceğini durumlarda bu yana "Bu nasıl biz her zaman böyle yapıldığı olduğundan" Merhaba mevcut işlem yerinde olabilir ya da ", bozuk olmayan bir şey varsa, neden Düzelt?". Etkilenen hello kişiler hello değişimin getireceği hello değeri toobe anlamak ve hello sorunları toobe Çözüldü hello önemini için teşekkür ederiz herhangi bir yeni aracın veya işlemin benimsenmesi her zaman en kolay yoludur.
* **Odağı tutma ilgili toodata varlıklar** -bir ekibin karşılaştığı hello iş sorunlarını ele alırken çok "Merhaba konuları Kes" ihtiyacınız ve ilgili tooleveraging kurumsal veri varlıkları nedir odaklanmasına daha fazla odağın.

Bazı örnek kullanım durumları ilgili tooData katalog şunlardır:

### <a name="example-use-cases"></a>Örnek kullanım durumları
* **Merkezi yüksek değerli veri kaynaklarını kaydetme** -BT hello kuruluş genelinde kullanılan veri kaynaklarını yönetir. BT, genel kurumsal veri kaynaklarını kaydederek ve bunlara açıklama ekleyerek Veri Kataloğu'nu kullanmaya başlayabilir.
* **Ekip tabanlı veri kaynaklarını kaydedin** - Farklı ekipler faydalı iş kolu veri kaynaklarına sahiptir. Kullanmaya başlama **Azure veri Kataloğu** tanımlayarak ve birçok farklı ekip ve yakalama hello ekibin bilgilerini de tarafından kullanılan önemli veri kaynaklarını kaydederek **Azure veri Kataloğu** ek açıklamaları.
* **Self servis iş zekası** - Ekipler, birden çok kaynaktan veri birleştirmeye çok fazla zaman ayırır. Kaydolun ve merkezi bir konum tooeliminate el ile veri kaynağı bulma işlemi veri kaynaklarına açıklama.

Veri Kataloğu senaryoları hakkında daha fazla tooread bkz [Azure veri Kataloğu genel senaryoları](data-catalog-common-scenarios.md).

Veri Kataloğu için birkaç kullanım durumu tanımlamanızın ardından, genel senaryolar ortaya çıkacaktır. nasıl tooidentify ilk pilot projenizi bir kullanım durumunu temel alarak Hello sonraki bölümde açıklanmaktadır.

## <a name="choose-a-data-catalog-pilot-project"></a>Veri Kataloğu pilot projesini seçme
Önemli bir başarı unsuru toosimplify ve başlangıç küçük ' dir. İyi tanımlanmış bir pilot kısıtlı kapsama yardımcı Koru hello ile çok karmaşık olan veya çok fazla katılımcı olan bir projeyle çıkmaza olmadan taşıma İleri yansıtın. Ancak, ayrıca önemli tooinclude kullanıcılardan erken Benimseyenler tooskeptics bir karışımını. Hello çözümünü benimsemeye kullanıcılar, gelecekteki iletişim ve hareket planınızı geliştirmenize yardımcı olur. Şüpheciler, engelleyici sorunları tanımlamanıza ve ele almanıza yardımcı olur. Şüpheciler kazananlara dönüşürken, geri bildirim tooidentify başarı sürücülerini kullanabilirsiniz.

Pilot planınız, veri Kataloğu ile tooachieve istediğiniz iş hedeflerini kademeli olarak sunmalıdır. Merhaba ilk Pilot projeyle bilgilerinizi ilerlettikçe, kullanıcı tabanınızı genişletebilirsiniz. İlk kapalı bir pilot proje, ölçülebilir başarının iyi tooestablish olmakla birlikte, hello nihai amacıyla organik veya viral büyümeye yöneliktir. Veri Kataloğu organik büyümesiyle kullanıcılar kendi veri kullanımı denetimindeki ve etkileyebileceğiniz ve diğerleri teşvik tooadopt ve toohello katalog katkıda.

### <a name="target-hello-right-team"></a>Hedef hello doğru ekibi
Pilot projenizi seçtiğinizde, var olan bir iş sorununu çözen hello en cazip senaryolara sahip ekibi seçin. Örneğin, bir iş analistinin SQL Server veritabanından rapor oluşturması. Merhaba sorunu aynen yalnızca tooseveral iş arkadaşlarınızı görüştükten sonra hello veri kaynağından haberdar olmuş olmasıdır. Son olarak, bunları bir Excel çalışma kitabı hakkında bulmuş toouse, hangi veri kaynakları zaman çalışırken toofind kaybettikten sonra her veri kaynağının açıklamasını içerir. Merhaba Excel çalışma kitabı ihtiyaç duyacağı hello tabloları yeterli açıklansa da, kayıtlı ve içinde açıklanan durumunda bunları hızlı bir şekilde bu veri kaynaklarının bulmuş olacaktı **Azure veri Kataloğu**.

### <a name="identify-data-heroes"></a>Veri hero'larını tanımlama
İçin ilk projeniz, veri üreten ve böylece hello takım bir sunuma sahip veri tüketen birkaç kişi olması gerekir.

**Veri Üreticileri** veri kaynakları hakkında uzmanlığı olan kişilerdir. Örneğin, başka bir ekipte bulunan David, Adventure Works'ün önemli veri kaynaklarıyla kapsamlı olarak çalışmıştır. Önceki toohello benimsenmesi **Azure veri Kataloğu**, David, Adventure Works veri kaynaklarını bir Excel çalışma kitabı toocapture bilgilerini oluşturdu.

**Veri tüketicileri** iş sorunlarını hello veri toosolve hello kullanımı ile ilgili uzmanlığı olan kişilerdir. Örneğin, Nancy iş analisti Adventure Works SQL Server veri kaynaklarını tooanalyze verileri otomatik olarak bağlanır.

Merhaba iş sorunlardan biri, **Azure veri Kataloğu** çözdü tooconnect olan **veri üreticileri** çok**veri tüketicileri**. Bunu, kurumsal veri kaynakları hakkındaki bilgiler için merkezi bir depo görevi görerek gerçekleştirir. David, Veri Kataloğu'nu kullanarak Adventure Works ve SQL Server veri kaynaklarını kaydeder. Bu veri kaynağını bulan herhangi bir kullanıcı kitle kaynak olanağını kullanarak hello verilere ilişkin görüşlerini paylaşabilir, ayrıca toousing hello veri bulduğu. Örneğin, Nancy hello katalogda arama yaparak hello veri kaynaklarını bulur ve hello verilerle ilgili Uzman bilgilerini paylaşır.  Şimdi, diğerleri hello kuruluşunuzdaki hello veri kataloğu arama yaparak paylaşılan yararlanır.

* veri kaynaklarını kaydetme hakkında daha fazla toolearn bkz [veri kaynaklarını kaydetme](data-catalog-get-started.md).
* veri kaynaklarını bulma hakkında daha fazla toolearn bkz [veri kaynaklarını arama](data-catalog-get-started.md).

### <a name="start-small-and-focused"></a>Küçük ve odaklı bir başlangıç
Çoğu Kurumsal pilot projede için iş kullanıcılarının veri Kataloğu hello değerini hızlı bir şekilde görebilmeniz için hello Kataloğu yüksek değerli veri kaynakları ile çekirdek. BT olduğu ilgi tooyour pilot ekibi olacak genel veri kaynakları tanımlayan bir iyi toostart. SQL Server gibi desteklenen veri kaynakları için hello kullanmanızı öneririz **Azure veri Kataloğu** veri kaynağı kayıt aracını. Merhaba veri kaynağı kayıt aracını, çok çeşitli SQL Server ve Oracle veritabanları dahil olmak üzere veri kaynaklarını kaydedebilirsiniz ve SQL Server Reporting Services raporları. Geçerli veri kaynaklarının tam listesi için bkz. [Azure Veri Kataloğu desteklenen veri kaynakları](data-catalog-dsr.md).

Belirledikten ve önemli veri kaynaklarını kayıtlı sonra başka konumlarda depolanan olası tooalso alma veri kaynağı açıklamalarının var. Merhaba veri Kataloğu API'si, geliştiricilerin tooload açıklamaları ve ek açıklamaları hello David oluşturduğu ve bakımını yaptığı Excel çalışma gibi başka bir konumdan sağlar.

Merhaba sonraki bölümde hello Adventure Works şirketine ait bir örnek proje açıklanmaktadır.

### <a name="an-example-project"></a>Örnek proje
Bu örnekte, Nancy hello iş analisti, bir SQL Server veritabanındaki verileri kullanarak ekibi için raporlar oluşturur. Merhaba sorunu aynen yalnızca tooseveral iş arkadaşlarınızı görüştükten sonra hello veri kaynağından haberdar olmuş olmasıdır. Bu veri kaynaklarının **Azure Veri Kataloğu** gibi merkezi bir konumda kayıtlı ve açıklama eklenmiş olarak bulunması durumunda bunları hızlı bir şekilde bulmuş olacaktı.

tooillustrate nasıl kolayca Nancy ve ekibinin yüksek değerli verileri bulmak için hello veri kaynakları hakkında bilgi (meta verileri) ile Merhaba veri kaynağı kayıt aracını toopopulate hello katalog kullanın. Bu şekilde hello hello veritabanı hakkında kullanılabilir toohello ekibi ve hello enterprise, değil yalnızca birkaç kişi bilgilerdir. Veri kaynakları Veri Kataloğu'na kaydedildikten sonra, Nancy ve ekibi bunları kolayca kullanabilir. Merhaba, her takım ve hello kuruluş için daha kapsamlı ve ilgili veri Kataloğu sonucudur. Daha fazla ekibe veri Kataloğu benimsemeyi gibi iş veri kaynaklarını daha kolay toofind ve kullanım haline gelir; Bu nedenle, daha veri merkezli bir kültüre tooachieve verilerinizle daha fazla etkinleştirme.

toolearn hello veri kaynağı kayıt aracını hakkında daha fazla bilgi görmek [Azure veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md).

Merhaba pilot projenin bir parçası olarak Nancy'nin ekibi Ayrıca, David bir Excel çalışma kitabında açıklanan veri kaynaklarını kullanır ve iş arkadaşlarının bakımını yaptığı. Hello kuruluştaki diğer ekipler de Excel çalışma kitaplarını toodescribe veri kaynakları kullandığından, BT Ekibi hello toocreate aracı toomigrate hello Excel çalışma kitabı tooData katalog karar verir. Merhaba veri Kataloğu REST API'si tooimport var olan ek açıklamaları kullanılarak hello pilot proje ekibi hello veri kaynağı kayıt aracını bilgilerle tam kullanarak hello veri kaynaklarından ayıklanan meta verileri içeren bir eksiksiz veri Kataloğu olabilir Merhaba gerek olmadan el ile yeniden giriş için veri üreticileri ve tüketicileri tarafından önceden belgelenmiş. Merhaba kurumsal veri Kataloğu büyüdükçe hello kuruluş ortak veri kaynakları ve özel kaynaklar ile genel olmayan senaryolar için veri Kataloğu API'si hello hello veri kaynağı kayıt aracını kullanabilirsiniz.

> [!NOTE]
> Merhaba kullanan bir örnek araç yazdığımız **Azure veri Kataloğu** API toomigrate bir Excel çalışma kitabı tooData Kataloğu. hello veri Kataloğu API'si ve hello örnek araç hakkında toolearn [hello geçici çalışma kitabı kod örneğini indirebilir](https://azure.microsoft.com/documentation/samples/data-catalog-dotnet-excel-register-data-assets/)ve hello denetleyin [Azure veri Kataloğu REST API'si](https://msdn.microsoft.com/library/azure/mt267593.aspx) belgeleri.
>
>

Merhaba pilot proje yerinde olduktan sonra saat tooexecute olduğundan, veri Kataloğu benimseme planı.

### <a name="execute"></a>Yürütme
Bu aşamada, Veri Kataloğu için kullanım durumlarını ve ilk projenizi tanımlamış durumdasınız. Ayrıca, hello anahtar Adventure Works veri kaynaklarını kaydettiniz ve bilgi eklediğiniz hello mevcut Excel çalışma kitabından yerleşik onun aracı hello kullanarak. Bu zaman toowork hello pilot ekip toostart hello veri Kataloğu benimseme işlemini ile sunulmuştur.

Başlattığınız bazı ipuçları tooget şunlardır:

* **Heyecan yaratın** - İş kullanıcıları, **Azure Veri Kataloğu**'nun hayatlarını kolaylaştırdığına inanmaları hâlinde heyecan duyar. Merhaba çözüm ve sağladığı hello avantajları hello teknolojiyi değil geçici toomake hello konuşma deneyin.
* **Değişimi kolaylaştırın** - küçük başlayın ve hello plan toobusiness kullanıcıları iletişim kurar. toobe başarılı, böylece hello sonucu etkiler ve sahipliği hello çözümü hakkında bir fikir geliştirmek hello başlayan gelen önemli tooinvolve users'dır.
* **Bölümlendirmek erken Benimseyenler** -erken Benimseyenler olan ne yaptıklarını ve Çoğalması tooevangelize hello yararları hakkında tutkulu iş kullanıcıları **Azure veri Kataloğu** tootheir eşler.
* **Eğitim hedefleri** -işletme kullanıcılarının ihtiyaç tooknow veri Kataloğu hakkında her şeyi, bu nedenle eğitim tooaddress belirli ekip hedeflerine hedef. Odak kullanıcıların ne ve nasıl bazı görevlerinin değişebilir, tooincorporate **Azure veri Kataloğu** günlük rutinlerine.
* **İstekli toofail olması** - Merhaba, pilot hello istenen sonuçları elde yeniden ve alanları toochange - tooa büyük kapsamına geçmeden önce pilot hello düzeltme sorunlarını tanımlamak.

Pilot ekibiniz veri Kataloğu'nu kullanmaya atlar önce bir başlangıç zamanlama toodiscuss toplantı hello beklentileri pilot proje ve ilk eğitimi sağlamak.

### <a name="set-expectations"></a>Beklentileri belirleme
Beklenti ve hedeflerin belirlenmesi, iş kullanıcılarının belirli sonuçlara odaklanmasına olanak tanır. tookeep hello proje kanalında atamak normal (örneğin: günlük veya haftalık hello kapsam ve hello pilot süresini göre) ödevleri. Böylece iş kullanıcıları, Kurumsal verilere bilgilerini yararlanabilirsiniz, veri Kataloğu'nun en değerli özelliklerinden hello kitle kaynak veri varlıklarını biridir. İyi bir ev atama için her pilot ekip üyesinin tooregister ya da kullanılan en az bir veri kaynağına açıklama. Bkz: [veri kaynağını kaydetme](data-catalog-get-started.md) ve [nasıl tooannotate veri kaynakları](data-catalog-get-started.md).

Düzenli aralıklarla tooreview hello ekipte ile bazı hello açıklamalarının karşılar. Veri kaynakları ile ilgili etkili ek açıklamalar başarılı bir veri Kataloğu benimseme hello Kalp olduklarından merkezi bir konumda anlamlı veri kaynağı öngörüleri sağlarlar. Etkili ek açıklamalar olmadan, veri kaynakları hakkında bilgi hello kuruluş geneline dağılmış halde kalır. Bkz: [nasıl tooannotate veri kaynakları](data-catalog-get-started.md).

Ve, hello Merhaba projeyi test edecek nihai kullanıcılar bulabilir ve toouse ihtiyaç duydukları hello veri kaynaklarını anlamasına olup olmadığını. Pilot kullanıcıları gün tooday çalışmaları için kullandıkları hello veri kaynaklarının ilgili olduğundan hello katalog tooensure düzenli olarak test etmelidir. Gerekli veri kaynağı eksik veya düzgün açıklamalı olduğunda, bu anımsatıcı tooregister kullanılmalıdır ek veri kaynaklarını veya tooprovide ek açıklamaları. Bu yöntem yalnızca değer toohello pilot girişime eklemez ancak aynı zamanda hello pilot tamamlandıktan sonra tooother takımlar yürüten etkili alışkanlıkların oluşturur.

### <a name="provide-training"></a>Eğitim verme
Eğitim, yeterli tooget hello kullanıcılar başlatıldı ve toohello belirli hedeflere uyarlanmış olması ve hello pilot ekip üyelerinin düzeyini deneyimi. Eğitim ile başlatılan tooget hello hello adımlarda izleyin [Azure veri Kataloğu ile çalışmaya başlama](data-catalog-get-started.md) makalesi. Ayrıca, hello indirebilirsiniz [Azure veri Kataloğu Pilot proje eğitimi sunumunu](https://github.com/Azure-Samples/data-catalog-dotnet-get-started/blob/master/Azure%20Data%20Catalog%20Training.pptx?raw=true). Bu PowerPoint sunumu pilot ekip üyelerinin başlatılan giriş veri Kataloğu tooyour size yardımcı olmalıdır.

## <a name="conclusion"></a>Sonuç
Pilot ekibinizin oldukça düzgün çalıştığından ve ilk hedeflerinize ulaşmanızın sonra veri Kataloğu benimseme toomore takımlar genişletmeniz gerekir. Uygulama ve pilot proje tooexpand veri Kataloğu kullanımını kuruluşunuz genelinde öğrendiklerinizi daraltın.

kimin hello pilot projeye katılan hello erken Benimseyenler, veri Kataloğu'nu benimseme hello avantajları hakkında yararlı tooget hello sözcüğü olabilir. Veri Kataloğu ekiplerinin iş sorunlarını çözmesine, veri kaynaklarını daha kolay bulmasına ve kullandıkları hello veri kaynakları hakkında Öngörüler paylaşmak nasıl Yardım diğer ekiplerle paylaşabilir. Örneğin, hello Adventure Works pilot ekibindeki erken Benimseyenler başkalarının ne kadar kolay toofind bilgileri bir kez sabit toofind olan Adventure Works veri varlıkları ile ilgili olduğunu gösterir ve anlayın.

Bu makalede, kuruluşunuzda **Azure Veri Kataloğu** ile çalışmaya başlama konusu ele alınmıştır. Biz mümkün toostart veri Kataloğu pilot proje olduğunuz umuyoruz ve veri Kataloğu kullanımını kuruluşunuz genelinde genişletin.

## <a name="more-information-about-azure-data-catalog"></a>Azure Veri Kataloğu hakkında daha fazla bilgi
* [Azure Veri Kataloğu ürün sayfası](https://azure.microsoft.com/services/data-catalog/)
* [Azure Veri Kataloğu belgeleri](https://azure.microsoft.com/documentation/services/data-catalog/)
* [Azure Veri Kataloğu genel senaryoları](data-catalog-common-scenarios.md)
* [Veri kaynaklarını kaydetme](data-catalog-get-started.md)
* [Veri kaynaklarını arama](data-catalog-get-started.md)
* [Veri kaynaklarına açıklama ekleme](data-catalog-get-started.md)
* [Kitle kaynak meta verileri](data-catalog-get-started.md)
