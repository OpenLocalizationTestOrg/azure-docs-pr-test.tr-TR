---
title: "Azure AD Connect eşitleme: hello mimarisini anlama | Microsoft Docs"
description: "Bu konu Azure AD Connect eşitleme hello mimarisini açıklar ve hello açıklar kullanılan terimler."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 465bcbe9-3bdd-4769-a8ca-f8905abf426d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 9fb979fcf8feb7b4d406789102239480b0b4bc94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-architecture"></a>Azure AD Connect eşitleme: hello mimarisini anlama
Bu konu, Azure AD Connect eşitleme için hello temel mimarisini kapsar. Birçok yönden benzer tooits öncellerine MIIS 2003, ILM 2007 ve FIM 2010 olur. Azure AD Connect eşitleme bu teknolojiler hello evrimi ' dir. Tüm önceki teknolojiler hakkında bilginiz varsa, bu konuda Merhaba içeriğine olarak da bilinen tooyou olacaktır. Yeni toosynchronization varsa, bu konu, ilgilidir. Ancak olmadığından bu konuda toobe tooAzure AD Connect eşitleme (Bu konuda çağrılan eşitleme altyapısı) özelleştirmeleri yaparken başarılı gereksinim tooknow hello ayrıntılarını.

## <a name="architecture"></a>Mimari
Merhaba eşitleme altyapısı birden çok bağlı veri kaynaklarında saklanan nesneleri tümleşik bir görünümünü oluşturur ve bu veri kaynaklarında kimlik bilgilerini yönetir. Bu tümleşik görünüm bağlı veri kaynakları ve belirleyen kuralları kümesi alınan hello kimlik bilgileri tarafından belirlenen nasıl tooprocess bu bilgileri.

### <a name="connected-data-sources-and-connectors"></a>Bağlı veri kaynakları ve bağlayıcıları
Merhaba eşitleme altyapısı Active Directory veya bir SQL Server veritabanı gibi farklı veri depoları kimlik bilgilerini işler. Veritabanı benzer biçimde verileri düzenler ve standart veri erişim yöntemleri sağlayan her veri deposu, hello eşitleme altyapısı için olası bir veri kaynağı adaydır. Eşitleme altyapısı tarafından eşitlenen hello veri depoları çağrılır **bağlı veri kaynakları** veya **bağlı dizinleri** (CD).

Merhaba eşitleme altyapısı adlı bir modül içinde bağlı veri kaynağı ile etkileşim yalıtan bir **bağlayıcı**. Her bağlı veri kaynağı belirli bir bağlayıcı türü. Merhaba bağlayıcı çevirir gerekli işlemi bağlı veri hello hello biçimine kaynak anlar.

Bağlayıcılar, bağlı veri kaynağı ile (hem okuma ve yazma) tooexchange kimlik bilgileri API çağrıları yapma. Olası tooadd özel bir bağlayıcı da olan hello Genişletilebilir bağlantı framework kullanarak. Merhaba aşağıda bir bağlayıcı bağlı veri kaynağı toohello eşitleme altyapısının nasıl bağlanacağını gösterir.

![Arş1](./media/active-directory-aadconnectsync-understanding-architecture/arch1.png)

Veri her iki yönde akmasını sağlamak, ancak her iki yönde de aynı anda geçirilemez. Diğer bir deyişle, bir bağlayıcı yapılandırılmış tooallow veri tooflow hello bağlı veri kaynağı toosync altyapısı veya eşitleme altyapısı toohello bağlı veri kaynağı olabilir, ancak bu işlemler yalnızca biri bir nesne ve öznitelik için herhangi bir zamanda meydana gelebilir. Merhaba yönü farklı öznitelikler ve farklı nesneler için farklı olabilir.

bir bağlayıcı tooconfigure, toosynchronize istediğiniz hello nesne türlerini belirtin. Merhaba nesne türlerini belirtme hello hello eşitleme işlemine dahil nesnelerin kapsamını tanımlar. Merhaba sonraki adım bir öznitelik ekleme listesi olarak bilinen tooselect hello öznitelikleri toosynchronize olacaktır. Bu ayarları yanıt toochanges tooyour iş kuralları'nda dilediğiniz zaman değiştirilebilir. Hello Azure AD Connect Yükleme Sihirbazı'nı kullandığınızda, bu ayarları sizin için yapılandırılır.

tooexport nesneleri tooa bağlı veri kaynağı, hello özniteliği ekleme listesi en az içermelidir hello minimum öznitelikleri gerekli toocreate belirli bir nesneye bağlı veri kaynağı içinde yazın. Örneğin, hello **sAMAccountName** özniteliği içerilmelidir hello özniteliği ekleme listesi tooexport bir kullanıcı nesnesi tooActive Directory tüm kullanıcı nesneleri Active Directory'de olması gerektiğinden bir **sAMAccountName**  özniteliği tanımlanmamış. Merhaba Yükleme Sihirbazı'nı yeniden, bu yapılandırmayı sizin için yapar.

Hello bağlı veri kaynağı bölümleri veya kapsayıcıları tooorganize nesneleri gibi yapısal bileşenleri kullanılıyorsa hello bağlı veri kaynağı için belirli bir çözüm kullanılan alanlarında hello sınırlayabilirsiniz.

### <a name="internal-structure-of-hello-sync-engine-namespace"></a>Merhaba eşitleme altyapısı ad alanının iç yapısı
Merhaba tüm eşitleme altyapısı ad hello kimlik bilgilerini saklamak iki ad alanı oluşur. Merhaba iki ad alanları şunlardır:

* Merhaba bağlayıcı alanı (CS)
* Merhaba meta veri deposu (MV)

Merhaba **bağlayıcı alanı** hello özniteliği ekleme listesinde belirtilen bir bağlı veri kaynağı ve hello öznitelikleri nesnelerden belirlenmiş hello gösterimlerini içeren bir hazırlama alanının değil. Merhaba eşitleme altyapısı hello bağlı veri kaynağı ve toostage gelen değişiklikleri nelerin değiştiğini hello bağlayıcı alanı toodetermine kullanır. Hello eşitleme altyapısı dışarı aktarma toohello bağlı veri kaynağı için değişiklikleri giden hello bağlayıcı alanı toostage de kullanır. Merhaba eşitleme altyapısı ayrı bağlayıcı alanı her bağlayıcı için bir hazırlama alanının tutar.

Bir hazırlama alanının kullanarak hello eşitleme altyapısı bağlı hello veri kaynaklarından bağımsız kalır ve bunların kullanılabilirlik ve erişilebilirlik tarafından etkilenmez. Sonuç olarak, hello hazırlama alanında hello verileri kullanarak kimlik bilgileri herhangi bir anda işleyebilir. Merhaba eşitleme altyapısı hello bağlı veri kaynağı içinde hello son iletişim oturumu sona erdi veya bağlı veri kaynağı hello yalnızca hello değişiklikleri tooidentity bilgi gönderme henüz, hangi azaltır almadığını yaptığından yalnızca hello değişiklikler isteyebilir Merhaba eşitleme altyapısı hello bağlı veri kaynağı arasındaki ağ trafiğini Hello.

Ayrıca, eşitleme altyapısı hello bağlayıcı alanı aşamaları tüm nesneler hakkındaki durum bilgilerini depolar. Yeni veri alındığında eşitleme altyapısı hello veri eşitlenmiş olup olmadığını her zaman değerlendirir.

Merhaba **meta veri deposu** tüm birleştirilmiş nesneleri, tek bir genel, tümleşik görünümünü sağlayan birden çok bağlı veri kaynaklarından toplanan hello kimlik bilgilerini içeren bir depolama alanıdır. Meta veri deposu nesneler hello bağlı veri kaynakları ve toocustomize hello eşitleme işlemine izin veren kurallar kümesi alınan hello kimlik bilgilerini temel alınarak oluşturulur.

Merhaba aşağıdaki çizimde hello bağlayıcı alanı ad alanı ve ad alanında hello eşitleme altyapısı hello meta veri deposu gösterir.

![Arch2](./media/active-directory-aadconnectsync-understanding-architecture/arch2.png)

## <a name="sync-engine-identity-objects"></a>Eşitleme altyapısı kimlik nesneleri
Merhaba eşitleme Altyapısı'ndaki Hello nesne ya da hello bağlı veri kaynağı nesneleri gösterimlerini veya hello altyapısı eşitleme tümleşik görünüme sahiptir bu nesneler. Her eşitleme altyapısı nesnenin genel benzersiz tanıtıcısı (GUID) sahip olması gerekir. Veri bütünlüğü ve nesneleri arasındaki ilişkiler express GUID'ler sağlar.

### <a name="connector-space-objects"></a>Bağlayıcı alanı nesneleri
Eşitleme altyapısı bağlı veri kaynağı ile iletişim kurduğunda, hello bağlı veri kaynağındaki hello kimlik bilgilerini okur ve bu bilgileri toocreate hello kimlik nesne gösterimini hello bağlayıcı alanı kullanır. Oluşturun veya bu nesneleri ayrı ayrı silin. Ancak, bir bağlayıcı alanı içindeki tüm nesneler el ile silebilirsiniz.

Merhaba bağlayıcı alanı içindeki tüm nesneler iki özniteliklere sahiptir:

* Bir genel benzersiz tanımlayıcı (GUID)
* Ayırt edici ad (DN olarak da bilinir)

Merhaba bağlı veri kaynağı benzersiz öznitelik toohello nesnesi atar sonra hello bağlayıcı alanı nesne bir bağlantı özniteliği de sahip olabilir. Merhaba bağlayıcı öznitelik hello bağlı veri kaynağı bir nesneyi benzersiz olarak tanımlar. Merhaba eşitleme altyapısı hello bağlantı toolocate hello ilgili temsili bu nesnenin hello bağlı veri kaynağı kullanır. Eşitleme altyapısı bir nesnenin bu hello bağlantı değişiklikleri hiçbir zaman hello nesne hello ömrü boyunca varsayar.

Alındığında hello bağlayıcılar çoğunu bilinen benzersiz tanımlayıcı toogenerate bir bağlantı otomatik olarak her nesne için kullanın. Örneğin, Active Directory Bağlayıcısı hello hello kullanır **objectGUID** bir bağlayıcı özniteliği. Açıkça tanımlanmış benzersiz bir tanımlayıcı sağlamaz, bağlı veri kaynakları için bağlantı oluşturma hello bağlayıcı yapılandırmasının bir parçası belirtebilirsiniz.

Durumda hello bağlantı birinden oluşturulmuştur veya daha fazla benzersiz öznitelik bir nesnenin, ne hangi değişiklikleri ve, benzersiz olarak türü hello bağlayıcı alanı (örneğin, çalışan sayısını veya bir kullanıcı kimliği) hello nesnesinde tanımlar.

Bağlayıcı alanı nesne hello aşağıdakilerden biri olabilir:

* Hazırlama nesnesi
* Bir yer tutucu

### <a name="staging-objects"></a>Hazırlama nesneleri
Hazırlama nesne nesne türlerini hello bağlı veri kaynağından belirlenmiş hello örneğini temsil eder. Ayrıca toohello GUID ve hello ayırt edici adı, bir hazırlama nesnesi her zaman hello nesne türünü belirten bir değer gerekir.

Her zaman içe hazırlama nesneleri hello bağlantı özniteliği için bir değer var. Yeni eşitleme altyapısı tarafından sağlanan ve hello bağlı veri kaynağında oluşturulmakta hello işlemi hazırlama nesneleri hello bağlantı özniteliği için bir değer yok.

Hazırlama nesneleri ayrıca iş özniteliklerinin ve eşitleme altyapısı tooperform hello eşitleme işlemi tarafından gerekli işlem bilgilerini geçerli değerleri uygulayın. Nesne hazırlama hello üzerinde hazırlanmış güncelleştirme hello türünü belirten bayrakları işlem bilgilerini içerir. Hazırlama nesne yeni kimlik bilgileri henüz işlenmemiş hello bağlı veri kaynağından aldıysa hello nesnesi olarak işaretlenir **içeri aktarma bekleyen**. Hazırlama nesne henüz dışa aktarılan toohello bağlı veri kaynağı yapılmamış yeni kimlik bilgileri varsa, olarak işaretlenir **dışa aktarma bekleyen**.

Hazırlama bir nesne, bir içeri aktarma veya dışarı aktarma nesne olabilir. Merhaba eşitleme altyapısı hello bağlı veri kaynağından alınan nesne bilgileri kullanarak alma nesnesi oluşturur. Eşitleme altyapısı hello bağlayıcı seçili hello nesne türlerinden birini eşleşen yeni bir nesne hello varlığı hakkındaki bilgileri aldığında, hello bağlı veri kaynağı hello nesnesinde bir gösterimi olarak hello bağlayıcı alanı alma nesnesi oluşturur.

Aşağıdaki çizimde hello hello bağlı veri kaynağındaki bir nesneyi temsil eden alma nesnesi gösterir.

![Arch3](./media/active-directory-aadconnectsync-understanding-architecture/arch3.png)

Merhaba eşitleme altyapısı hello meta veri deposunda nesne bilgileri kullanarak bir dışarı aktarma nesnesi oluşturur. Dışa verilen toohello bağlı veri kaynağı hello sonraki iletişim oturumu sırasında nesneleridir. Merhaba açısından, hello eşitleme altyapısı dışarı aktarma nesneler hello bağlı veri kaynağı henüz yok. Bu nedenle, hello bağlayıcı öznitelik verme nesne için kullanılabilir değil. Eşitleme altyapısı hello nesne aldıktan sonra hello bağlı veri kaynağı hello nesnesinin hello bağlantı özniteliği için benzersiz bir değer oluşturur.

Merhaba aşağıdaki çizimde bir dışarı aktarma nesne hello meta veri deposunda kimlik bilgilerini kullanarak nasıl oluşturulacağını gösterir.

![Arch4](./media/active-directory-aadconnectsync-understanding-architecture/arch4.png)

Merhaba eşitleme altyapısı hello nesne hello bağlı veri kaynağından yeniden içe aktarılması hello verme hello nesnesinin onaylar. Eşitleme altyapısı bunları bu bağlı veri kaynağından hello İleri alma sırasında aldığında verme nesneleri içeri aktarma nesneler olur.

### <a name="placeholders"></a>Yer tutucuları
Merhaba eşitleme altyapısı düz ad alanı toostore nesneleri kullanır. Ancak, Active Directory gibi bazı bağlı veri kaynağı hiyerarşik bir ad kullanın. düz bir ad alanı içine tootransform bilgi hiyerarşik ad alanından, yer tutucular toopreserve hello hiyerarşisi eşitleme altyapısı kullanır.

Her bir yer tutucu eşitleme motoruna aktarılmadı ancak gerekli tooconstruct hello hiyerarşik adı olan bir nesnenin hiyerarşik adı bir bileşeninin (örneğin, bir kuruluş birimi) temsil eder. Bunlar hello bağlayıcı alanı nesne hazırlama değil hello bağlı veri kaynağı tooobjects başvurularında tarafından oluşturulan boşlukları doldurun.

Merhaba eşitleme altyapısı da değil henüz içeri aktarıldığını yer tutucuları başvurulan toostore nesneleri kullanır. Örneğin, eşitleme hello için yapılandırılmış tooinclude hello Yöneticisi özniteliği ise *Abbie Spencer* nesne ve hello alınan değeri henüz gibi alındı değil bir nesne *CN Lee Sperry, CN = kullanıcılar, DC = fabrikam = DC = com*, hello Yöneticisi bilgileri hello bağlayıcı alanı yer tutucu olarak depolanır. Hello Yöneticisi nesnesi daha sonra aldıysanız, hello yer tutucu nesne hello Yöneticisi temsil eden nesnesi hazırlama hello tarafından üzerine yazılır.

### <a name="metaverse-objects"></a>Meta veri deposu nesneleri
Bir meta veri deposu nesnesi toplanan hello görünümü içerir hello bağlayıcı alanı nesne hazırlama Merhaba, bu eşitleme altyapısı vardır. Eşitleme altyapısı alma nesneleri hello bilgileri kullanarak meta veri deposu nesnesi oluşturur. Birkaç bağlayıcı alanı nesne bağlantılı tooa tek meta veri deposu nesnesi olabilir, ancak bir bağlayıcı alanı nesne bir meta veri deposu nesnesi daha bağlantılı toomore olamaz.

Meta veri deposu nesneleri el ile oluşturulan veya silinemez. Merhaba eşitleme altyapısı, bir bağlantı tooany bağlayıcı alanı nesne hello bağlayıcı alanı yok meta veri deposu nesneleri otomatik olarak siler.

bağlı veri kaynağı tooa karşılık gelen nesne türü hello meta veri deposu içinde nesnelerinde toomap, nesne türleri ve ilişkili öznitelikleri önceden tanımlanmış bir dizi genişletilebilir bir şemayı eşitleme altyapısı sağlar. Yeni nesne türleri ve meta veri nesnelerinin öznitelikleri oluşturabilirsiniz. Tek değerli veya birden çok değerli öznitelikleri olabilir ve hello öznitelik türlerini dizeler, başvurular, sayıları ve Boole değerleri olabilir.

### <a name="relationships-between-staging-objects-and-metaverse-objects"></a>Hazırlama ve meta veri deposu nesneleri arasındaki ilişkiler
Merhaba eşitleme altyapısı ad içinde hello veri akışı hazırlama ve meta veri deposu nesneleri arasındaki hello bağlantı ilişki etkinleştirilir. Bağlantılı tooa meta veri deposu nesne adlı bir hazırlama diğer bir deyişle nesne bir **birleştirilmiş nesne** (veya **bağlayıcı nesnesi**). Bağlantılı tooa meta veri deposu nesnesi değil hazırlama bir nesne olarak adlandırılan bir **nesne üyeliğinden** (veya **ayırıcı nesne**). Merhaba koşulları birleştirilmiş ve üyeliğinden olan tercih edilen toonot karıştırır hello bağlayıcılar içeri aktarma ve bağlı bir dizinden verileri dışarı aktarma sorumlu ile.

Yer tutucuları bağlantılı tooa meta veri deposu nesne hiçbir zaman olan

Birleştirilmiş bir nesne, bir hazırlama nesnesi ve onun bağlı ilişkiyi tooa tek meta veri deposu nesnesi oluşur. Bağlayıcı alanı nesne bir meta veri deposu nesnesi arasındaki kullanılan toosynchronize öznitelik değerlerini birleştirilmiş nesneleridir.

Hazırlama nesne eşitleme sırasında birleştirilmiş bir nesne olduğunda öznitelikleri nesnesi ve hello meta veri deposu nesnesi hazırlama hello arasında akabilir. Öznitelik akışı yönlüdür ve içeri aktarma özniteliği kuralları ve dışarı aktarma özniteliği kuralları kullanılarak yapılandırılır.

Bir tek bağlayıcı alanı nesne bağlantılı tooonly bir meta veri deposu nesne olabilir. Bununla birlikte, her meta veri deposu nesnesi hello aşağıdaki çizimde gösterildiği gibi bağlantılı toomultiple bağlayıcı alanı nesneleri hello aynı veya farklı bağlayıcı alanları olabilir.

![Arch5](./media/active-directory-aadconnectsync-understanding-architecture/arch5.png)

Nesne hazırlama hello arasındaki ilişki Hello bağlı ve bir meta veri deposu nesnesi kalıcıdır ve belirlediğiniz kurallara göre kaldırılabilir.

Bağlantısı kesilmiş bir nesne olup olmadığını bağlantılı tooany meta veri deposu nesnesi hazırlama bir nesnedir. bağlantısı kesilmiş bir nesnenin değerlerini olmayan hello özniteliği hello meta veri deposu içinde daha fazla herhangi işlendi. öznitelik değerleri nesnesinin hello karşılık gelen hello bağlı veri kaynağı eşitleme altyapısı tarafından güncelleştirilmez hello.

Bağlantısı kesilmiş nesneler kullanarak, eşitleme altyapısında kimlik bilgilerini depolamak ve daha sonra işleme. Hello bağlayıcı alanı bağlantısı kesilmiş bir nesne olarak hazırlama nesnenin koruyarak birçok avantaj sunar. Hello sistem zaten bu nesnenin hakkında gerekli hello bilgi hazırlanan olduğundan, bu nesne bir gösterimini hello sırasında yeniden sonraki hello bağlı veri kaynağından almak gerekli toocreate değil. Geçerli bağlantı toohello bağlı veri kaynağı olsa bile bu şekilde, eşitleme altyapısı hello bağlı veri kaynağı, tam bir anlık görüntü her zaman vardır. Bağlantısı kesilmiş nesneleri birleştirilmiş nesnelere ve tersi yönde belirlediğiniz hello kurallara bağlı olarak dönüştürülebilir.

Alma nesnesi, bağlantısı kesilmiş bir nesne olarak oluşturulur. Bir verme nesne birleştirilmiş bir nesne olmalıdır. Merhaba sistem mantık bu kural zorlar ve birleştirilmiş bir nesne değil her dışarı aktarma nesneyi siler.

## <a name="sync-engine-identity-management-process"></a>Eşitleme altyapısı Kimlik Yönetimi işlemi
Merhaba Kimlik Yönetimi işlem kimlik bilgilerini farklı bağlı veri kaynakları arasında nasıl güncelleştirileceğini denetler. Kimlik Yönetimi üç işlemde oluşur:

* İçeri Aktarma
* Eşitleme
* Dışarı Aktarma

Hello içeri aktarma işlemi sırasında eşitleme altyapısı hello gelen kimlik bilgileri bağlı veri kaynağı olarak değerlendirilir. Değişiklikler algıladığında, bu yeni hazırlama nesneler oluşturur ya da eşitleme için hello bağlayıcı alanı mevcut hazırlama nesneleri güncelleştirir.

Merhaba eşitleme işlemi sırasında eşitleme altyapısı hello bağlayıcı alanı oluşmuş hello meta veri deposu tooreflect değişiklikleri güncelleştirir ve hello meta veri deposunda oluşmuş hello bağlayıcı alanı tooreflect değişiklikleri güncelleştirir.

Merhaba dışa aktarma işlemi sırasında eşitleme altyapısı nesneleri hazırlama hazırlanır ve dışarı aktarma gibi bekleyen işaretlenen değişiklikleri çıkışı iter.

Aşağıdaki çizimde hello hello işlemler her bir bağlı veri kaynağı tooanother kimlik bilgileri akışları nerede oluştuğunu gösterir.

![Arch6](./media/active-directory-aadconnectsync-understanding-architecture/arch6.png)

### <a name="import-process"></a>İçeri aktarma işlemi
Merhaba içeri aktarma işlemi sırasında eşitleme Altyapısı güncelleştirmeleri tooidentity bilgileri değerlendirir. Eşitleme altyapısı hazırlama nesne hakkında hello kimlik bilgileriyle hello bağlı veri kaynağından alınan hello kimlik bilgilerini karşılaştırır ve nesne hazırlama hello güncelleştirmeleri gerekli olup olmadığını belirler. Yeni veri nesnesiyle hazırlama gerekli tooupdate hello ise, nesne hazırlama hello gibi içeri aktarma bekleyen işaretlenir.

Eşitleme altyapısı eşitleme önce hello bağlayıcı alanı nesne hazırlama göre değişen hello kimlik bilgileri işleyebilir. Bu işlem, hello aşağıdaki avantajları sunar:

* **Verimli eşitleme**. Eşitleme sırasında işlenen veri miktarı Hello en aza indirilir.
* **Verimli yeniden eşitleme**. Eşitleme altyapısı olmadan yeniden bağlanan hello eşitleme altyapısı toohello veri kaynağı kimlik bilgilerini nasıl işlediği değiştirebilirsiniz.
* **Fırsat toopreview eşitleme**. Merhaba Kimlik Yönetimi işlem hakkında varsayımlar doğru eşitleme tooverify önizleyebilirsiniz.

Merhaba bağlayıcı belirtilen her nesne için hello eşitleme altyapısı toolocate hello bağlayıcı hello bağlayıcı alanı hello nesnesinde bir gösterimini önce çalışır. Eşitleme altyapısı hello bağlayıcı alanı hazırlama tüm nesneleri inceler ve toofind eşleşen bir bağlantı özniteliğine sahip karşılık gelen bir hazırlama nesnesini çalışır. Varolan hazırlama nesnesi yok eşleşen bir öznitelik bağlantı, eşitleme altyapısı çalıştığında toofind hello karşılık gelen hazırlama nesnesiyle varsa aynı ayırt edici adı.

Eşitleme altyapısı yer işaretine göre değil ancak ayırt edici adı ile eşleşen hazırlama bir nesne bulduğunda, hello aşağıdaki özel davranış oluşur:

* Merhaba bağlayıcı alanı bulunan hello nesnesi sahip hiçbir bağlantı sonra eşitleme altyapısı bu nesne hello bağlayıcı alanından kaldırır ve işaretleri meta veri deposu nesne hello bağlantılı tooas olmasına **sonraki eşitlemeyi Çalıştır sağlama yeniden**. Daha sonra hello yeni alma nesnesi oluşturur.
* Merhaba nesne Hello bağlayıcı alanı bulunan bir bağlantı varsa, eşitleme altyapısı bu nesne ya da yeniden adlandırılmış veya silinmiş hello bağlı dizininde olduğunu varsayar. Böylece hello gelen nesne yerleştirebilirsiniz hello bağlayıcı alanı nesne için bir geçici, yeni ayırt edici ad atar. Merhaba eski nesnesi daha sonra olur **geçici**, hello bağlayıcı tooimport hello yeniden adlandırma veya silme tooresolve hello durum bekleniyor.

Eşitleme altyapısı hello bağlayıcı belirtilen toohello nesne karşılık gelen hazırlama bir nesne bulur ne tür bir değişiklik tooapply belirler. Örneğin, eşitleme altyapısı yeniden adlandırın veya hello bağlı veri kaynağı hello nesnesinde silin veya yalnızca hello nesnenin öznitelik değerlerini güncelleştirebilir.

Güncelleştirilen verileri hazırlama nesneleriyle bekleyen alma olarak işaretlenir. İçeri aktarmalar bekleyen farklı türleri kullanılabilir. Hello içeri aktarma işleminin sonucunu Hello bağlı olarak, şu bekleyen alma türlerini hello birini hello bağlayıcı alanı hazırlama nesnesinde sahiptir:

* **None**. Hiçbir değişiklik tooany nesne hazırlama hello hello özniteliklerin kullanılabilir. Eşitleme altyapısı, bu tür olarak içeri aktarma bekleyen işaretlemez.
* **Ekleme**. Nesne hazırlama hello hello bağlayıcı alanı içinde yeni bir alma nesnesidir. Eşitleme altyapısı bu tür alma gibi ek işleme hello meta veri deposu için bekleyen işaretler.
* **Güncelleştirme**. Eşitleme altyapısı karşılık gelen hazırlama nesnesini hello bağlayıcı alanı bulur ve böylece güncelleştirmeleri toohello öznitelikleri hello meta veri deposunda işlenebilir içeri aktarma bekleyen bu türü olarak işaretler. Nesnesini yeniden adlandırma güncelleştirmeleri içerir.
* **Silme**. Eşitleme altyapısı karşılık gelen hazırlama nesnesini hello bağlayıcı alanı bulur ve böylece hello birleştirilmiş nesne silinebilir içeri aktarma bekleyen bu türü olarak işaretler.
* **Silme ve ekleme**. Eşitleme altyapısı karşılık gelen hazırlama nesnesini hello bağlayıcı alanı bulur ancak hello nesne türleri eşleşmiyor. Bu durumda, bir değişiklik hazırlanan delete ekleme. Bir silme-ekleyin değişikliği hello nesne türü değiştiğinde farklı kural kümesini toothis nesnesinin geçerli olduğundan, bu nesnenin tam bir eşitleme gerçekleşmelidir toohello eşitleme altyapısı gösterir.

Ayarı hazırlama bir nesnenin alma durumu bekleyen hello tarafından mümkündür tooreduce önemli ölçüde hello çünkü bunu yaparsanız, hello sistem tooprocess kadar veri güncelleyen nesneleri izin verir. eşitleme sırasında işlenen veri miktarı.

### <a name="synchronization-process"></a>Eşitleme işlemi
Eşitleme iki ilgili işlemden oluşur:

* Merhaba meta veri deposu Merhaba içeriğine hello bağlayıcı alanı hello verileri kullanarak güncelleştirildiğinde eşitleme, gelen.
* Merhaba bağlayıcı alanı Merhaba içeriğine hello meta veri deposunda verileri kullanarak güncelleştirildiğinde giden eşitleme.

Merhaba bağlayıcı alanı hazırlanan hello bilgileri kullanarak, hello gelen eşitleme işlemi hello meta veri deposu tümleşik hello bağlı hello veri kaynaklarında saklanan hello verilerin görünümünü oluşturur. Merhaba kuralların nasıl yapılandırıldığına bağlı olarak tüm hazırlama nesneleri veya yalnızca bir bekleyen alma bilgileri toplanır.

meta veri deposu nesnelerini değiştirdiğinizde hello giden eşitleme işlemi güncelleştirmeleri nesnelerini dışa aktarın.

Gelen eşitleme bağlı hello veri kaynaklarından alınan hello kimlik bilgisinin hello meta dizesinde tümleşik hello görünümü oluşturur. Eşitleme altyapısı, hello veri kaynağına bağlandı hello son kimlik bilgilerini kullanarak kimlik bilgileri herhangi bir anda işleyebilir.

**Gelen eşitleme**

Gelen eşitleme işlemlerini takip hello içerir:

* **Sağlama** (olarak da bilinir **projeksiyon** bu işlemden önemli toodistinguish ise giden Eşitleme sağlama). Merhaba eşitleme altyapısı hazırlama nesnesini temel alan yeni bir meta veri deposu nesnesi oluşturur ve bunları bağlar. Sağlama nesne düzeyinde bir işlemdir.
* **Katılma**. Merhaba eşitleme altyapısı, bir hazırlama nesne tooan var olan meta veri deposu nesnesi bağlar. Bir birleştirme nesne düzeyinde bir işlemdir.
* **Öznitelik akışı alma**. Eşitleme altyapısı hello meta veri deposu hello nesnesinin öznitelik akışı olarak adlandırılan hello öznitelik değerleri güncelleştirir. İçeri aktarma öznitelik akışı hazırlama nesnesi ve bir meta veri deposu nesnesi arasında bir bağlantı gerektiren bir öznitelik düzeyi işlemdir.

Sağlama hello meta veri deposunda nesneleri oluşturur hello yalnızca işlemidir. Sağlama, bağlantısı kesilmiş nesneleri içeri aktarma nesneleri etkiler. Sağlama sırasında eşitleme altyapısı hello alma nesnenin nesne türü toohello karşılık gelir ve hem nesneleri, böylece birleştirilmiş bir nesne oluşturma arasında bir bağlantı kurar bir meta veri deposu nesnesi oluşturur.

Merhaba katılma işlemi de nesneleri içeri aktar ve meta veri deposu nesnesi arasında bir bağlantı kurar. katılma ve sağlama Hello birbirinden hello birleştirme işlemi hello alma nesne olan hello sağlama işlemini yeni bir meta veri deposu nesnesi oluşturur bağlantılı tooan var olan meta veri deposu nesnesi gerektirmesidir.

Eşitleme altyapısı toojoin alma nesne tooa meta veri deposu nesnesi hello eşitleme kuralı yapılandırmasında belirtilen ölçütleri kullanarak çalışır.

Merhaba sağlama ve birleştirme işlemleri sırasında eşitleme altyapısı onları birleştirilmiş bir yarıçap nesne tooa meta veri deposu nesnesi bağlar. Bu nesne düzeyinde işlemler tamamlandıktan sonra eşitleme altyapısı hello öznitelik değerleri hello ilişkili meta veri deposu nesnesinin güncelleştirebilirsiniz. Bu işlem, içeri aktarma öznitelik akışı olarak adlandırılır.

İçeri aktarma öznitelik akışı, yeni veri taşıyan ile bağlantılı tooa meta veri deposu nesnesi tüm alma nesnelerinde oluşur.

**Giden eşitleme**

Bir meta veri deposu nesnesi değiştirmek ancak silinmez giden eşitleme güncelleştirmeleri nesnelerini dışa aktarın. Giden eşitleme hello amacı tooevaluate olup güncelleştirmeleri toostaging hello bağlayıcı alanları nesnelerindeki değişiklikler toometaverse nesneler gerektirir. Bazı durumlarda, değişiklikleri hazırlama boşluklar bağlayıcı nesnelerini gerektirebilir hello güncelleştirilmesi. Değiştirilen hazırlama nesneleri, onları nesneleri dışarı verme gibi bekleyen işaretlenir. Nesneleri toohello bağlı veri kaynağı hello dışa aktarma işlemi sırasında Kalan daha sonra bu dışarı aktarma.

Giden eşitleme üç işlem vardır:

* **Sağlama**
* **Sağlama kaldırma**
* **Öznitelik akışı dışarı aktarma**

Sağlama ve sağlamayı kaldırma her iki nesne düzeyinde işlemleridir. Sağlamayı kaldırmayı yalnızca sağlama işlemi başlatabilirsiniz çünkü sağlama üzerinde bağlıdır. Sağlamayı kaldırmayı bir meta veri deposu nesnesi ve bir verme nesnesi arasındaki kaldırır hello bağlantı sağlama geldiğinde tetiklenir.

Sağlama, her zaman değişikliklerin hello meta dizesinde uygulanan tooobjects durumlarda tetiklenir. Toometaverse nesneler değişiklik yapıldığında, eşitleme altyapısı sağlama işlemi hello bir parçası olarak görevleri aşağıdaki hello birini gerçekleştirebilirsiniz:

* Bir meta veri deposu nesnesi yeni oluşturulan bağlantılı tooa verme nesne olduğu katılan nesnelerini oluşturun.
* Birleştirilmiş bir nesne yeniden adlandırın.
* Bir meta veri deposu nesnesi ve nesneleri, bağlantısı kesilmiş bir nesne oluşturma hazırlama arasındaki bağlantıları çıkarın.

Sağlama eşitleme altyapısı toocreate yeni bir bağlayıcı nesnesi gerektiriyorsa, hello nesne hello bağlı veri kaynağında henüz mevcut olmadığından nesne toowhich hello meta veri deposu nesnesi hazırlama hello olduğu bağlı her zaman bir dışarı aktarma nesnesidir.

Sağlama eşitleme altyapısı toodisjoin bağlantısı kesilmiş bir nesne oluşturma birleştirilmiş bir nesneyi gerektirirse sağlamayı tetiklenir. işlem sağlamayı hello hello nesneyi siler.

Sağlama kaldırma sırasında bir dışa aktarma nesne silme fiziksel olarak hello nesne silmez. Merhaba nesnesi olarak işaretlenir **silinmiş**, o hello silme işlemi başka bir deyişle, hello nesnesinde hazırlanır.

Dışarı aktarma öznitelik akışı da hello giden eşitleme işlemi sırasında oluşur öznitelik akışı alma benzer toohello şekilde gelen eşitleme sırasında oluşur. Dışarı aktarma öznitelik akışı katılan yalnızca meta veri deposu ve dışarı aktarma nesneler arasında oluşur.

### <a name="export-process"></a>Dışa aktarma işlemi
Hello dışa aktarma işlemi sırasında eşitleme altyapısı verme gibi hello bağlayıcı alanındaki bekleyen işaretlenen tüm verme nesneleri inceler ve ardından veri kaynağını gönderir güncelleştirmeleri toohello bağlı.

Merhaba eşitleme altyapısı verme hello başarısını belirleyebilir ancak yeterince hello Kimlik Yönetimi işleminin tamamlandığını belirleyemiyor. Merhaba bağlı veri kaynağı nesneleri her zaman başka işlemler tarafından değiştirilebilir. Eşitleme altyapısı kalıcı bağlantı toohello bağlı veri kaynağı olmadığından, yalnızca bir başarılı aktarma bildirim dayalı hello bağlı veri kaynağı bir nesnenin hello özellikleri hakkında yeterli toomake varsayımlar değil.

Örneğin, değişiklik hello nesnesinin öznitelikleri geri tootheir özgün değerler hello bir işlemde veri kaynağı bağlı (hemen hello veri out eşitleme altyapısı tarafından ve başarılı bir şekilde itildiği sonra başka bir deyişle, hello bağlı veri kaynağı hello değerleri üzerine yazabilir "Hello bağlı veri kaynağında uygulanır).

Eşitleme altyapısı depoları verme hello ve hazırlama her nesne hakkındaki durum bilgilerini alın. Merhaba özniteliği ekleme listesinde belirtilen hello özniteliklerinin değerlerini hello son verme itibaren değişip değişmediğini alma depolanmasını hello ve durum etkinleştirir eşitleme altyapısı tooreact uygun şekilde verin. Eşitleme altyapısı dışarı aktarılan toohello bağlı veri kaynağı olan hello alma işlemi tooconfirm, öznitelik değerleri kullanır. Merhaba arasında bir karşılaştırma içe ve dışa aktarılan bilgileri hello aşağıdaki çizimde gösterildiği gibi eşitleme altyapısı toodetermine hello dışarı aktarma başarılı olup olmadığını veya yinelenen toobe gerekip gerekmediğini sağlar.

![Arch7](./media/active-directory-aadconnectsync-understanding-architecture/arch7.png)

Örneğin, öznitelik değeri 5 olan C eşitleme altyapısı dışarı verirse tooa bağlı veri kaynağı, C = 5, verme durumu bellekte depolar. Eşitleme altyapısı (diğer bir deyişle, farklı bir değer son alınan sürece bu değer kalıcı olarak uygulanan toohello nesne yedeklenmedi varsayar çünkü her ek verme Bu nesne üzerinde bir girişim tooexport C = 5 toohello bağlı veri kaynağında yeniden sonuçları "Hello veri kaynağı bağlı). C = 5 hello nesne üzerinde bir içeri aktarma işlemi sırasında alındığında hello verme bellek temizlenir.

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [Azure AD Connect eşitleme](active-directory-aadconnectsync-whatis.md) yapılandırma.

[Şirket içi kimliklerinizi Azure Active Directory ile tümleştirme](active-directory-aadconnect.md) hakkında daha fazla bilgi edinin.

