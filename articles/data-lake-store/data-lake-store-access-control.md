---
title: "erişim denetimi Data Lake Store'da aaaOverview | Microsoft Docs"
description: "Azure Data Lake Store’da erişim denetiminin çalışma şekli hakkında bilgi edinin"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a>Azure Data Lake Store’da erişim denetimi

Azure Data Lake Store sırayla hello POSIX erişim denetimi modeli türetilen HDFS türeyen bir erişim denetimi modeli uygular. Bu makalede hello erişim denetimi modeli Data Lake Store için hello temelleri özetlenmektedir. toolearn hello HDFS erişim denetimi modeli hakkında daha fazla bilgi görmek [HDFS izinleri Kılavuzu](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).

## <a name="access-control-lists-on-files-and-folders"></a>Dosyalar ve klasörler üzerindeki erişim denetimi listeleri

İki tür erişim denetim listesi (ACL) vardır: **Erişim ACL’leri** ve **Varsayılan ACL’ler**.

* **Erişim ACL'ler**: Bu denetim erişim tooan nesnesi. Hem dosyalar hem de klasörler Erişim ACL’lerine sahiptir.

* **Varsayılan ACL'leri**: "Bu klasörü altında oluşturulan tüm alt öğeleri için hello erişim ACL'ler belirleyen bir klasörle ilişkili şablonu" ACL'leri. Dosyalar Varsayılan ACL’ye sahip değildir.

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

Erişim ACL'ler ve varsayılan ACL'leri sahip hello aynı yapısı.

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> Bir üst hello varsayılan ACL değişen hello erişim ACL veya varsayılan ACL zaten alt öğelerinin etkilemez.
>
>

## <a name="users-and-identities"></a>Kullanıcılar ve kimlikler

Her dosya ve klasör bu kimlikler için farklı izinlere sahiptir:

* sahibi olan kullanıcı hello dosyasının hello
* Merhaba sahibi olan Grup
* Adlandırılmış kullanıcılar
* Adlandırılmış gruplar
* Diğer tüm kullanıcılar

Merhaba kimlikleri kullanıcıların ve grupların Azure Active Directory (Azure AD) hesaplardır. Aksi belirtilmediği sürece, bir "kullanıcı" Merhaba bağlamındaki Data Lake Store, bu nedenle herhangi bir Azure AD kullanıcısının veya bir Azure AD güvenlik grubuna anlamına gelir.

## <a name="permissions"></a>İzinler

bir dosya sistemi nesnenin Hello izinleri olan **okuma**, **yazma**, ve **yürütme**, ve dosya ve klasörleri aşağıdaki tablonun hello gösterildiği gibi kullanılabilmesi için:

|            |    Dosya     |   Klasör |
|------------|-------------|----------|
| **Okuma (R)** | Bir dosyanın içeriğini Hello okuyabilir | Gerektirir **okuma** ve **yürütme** toolist hello hello klasörünün içeriğini|
| **Yazma (W)** | Yazma veya tooa dosya ekleme | Gerektirir **yazma** ve **yürütme** klasöründeki toocreate alt öğeleri |
| **Yürütme (X)** | Data Lake Store hello bağlamında herhangi bir şey gelmez | Bir klasörün gerekli tootraverse hello alt öğeleri |

### <a name="short-forms-for-permissions"></a>İzinlerin kısaltmaları

**RWX** kullanılan tooindicate olan **okuma + yazma + yürütme**. Daha fazla sıkıştırılmış bir sayısal form bulunduğu **okuma = 4**, **yazma = 2**, ve **Execute = 1**, hangi hello toplamını hello izinleri temsil eder. Bazı örnekler aşağıda verilmiştir.

| Sayısal biçim | Kısa biçim |      Anlamı     |
|--------------|------------|------------------------|
| 7            | RWX        | Okuma + Yazma + Yürütme |
| 5            | R-X        | Okuma + Yürütme         |
| 4            | R--        | Okuma                   |
| 0            | ---        | İzin yok         |


### <a name="permissions-do-not-inherit"></a>İzinler devralınmaz

Data Lake Store tarafından kullanılan hello POSIX tipi modelinde, bir öğe için izinleri hello öğede depolanır. Diğer bir deyişle, bir öğe için izinleri hello üst öğelerinden devralınan olamaz.

## <a name="common-scenarios-related-toopermissions"></a>Yaygın senaryolar ilgili toopermissions

Şunlardır anlamak hangi izinlerin olduğunu bazı ortak senaryolar toohelp belirli işlemlerin bir Data Lake Store hesabındaki tooperform gerekli.

### <a name="permissions-needed-tooread-a-file"></a>Bir dosya tooread gereken izinler

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* Okuma hello dosya toobe için hello çağıran gereksinimlerini **okuma** izinleri.
* Tüm hello dosyasını içeren hello Klasör yapısındaki klasörler hello için hello çağıran gereksinimlerini **yürütme** izinleri.

### <a name="permissions-needed-tooappend-tooa-file"></a>Tooappend tooa dosya gereken izinler

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* Merhaba dosya toobe eklenen için hello çağıran gereksinimlerini **yazma** izinleri.
* Tüm hello dosya içeren klasörleri hello için hello çağıran gereksinimlerini **yürütme** izinleri.

### <a name="permissions-needed-toodelete-a-file"></a>Bir dosya toodelete gereken izinler

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* Merhaba üst klasör için hello çağıran gereksinimlerini **yazma + yürütme** izinleri.
* Tüm diğer hello dosyanın yolu klasörlerde hello için hello çağıran gereksinimlerini **yürütme** izinleri.



> [!NOTE]
> Merhaba dosyanın izinlerini önceki iki koşul hello sürece bunu true gerekli toodelete olmayan yazma.
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a>Bir klasör tooenumerate gereken izinler

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* Başlangıç klasörü tooenumerate için hello çağıran gereksinimlerini **okuma + yürütme** izinleri.
* Tüm üst klasörlerin hello için hello çağıran gereksinimlerini **yürütme** izinleri.

## <a name="viewing-permissions-in-hello-azure-portal"></a>Hello Azure portalı izinlerini görüntüleme

Merhaba gelen **Veri Gezgini** hello Data Lake Store hesabı dikey tıklayın **erişim** toosee hello ACL'ler bir dosya veya klasör. Tıklatın **erişim** toosee Merhaba ACL'ler hello **katalog** hello altında bir klasör **mydatastore** hesabı.

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

Bu dikey penceresinde hello üst kısmında elinizde hello izinleri genel bir bakış gösterilir. (Merhaba ekran görüntüsünde, hello Bob kullanıcıdır.) Hello erişim izinleri gösterilir. Bundan sonra gelen hello **erişim** dikey penceresinde tıklatın **Basit Görünüm** toosee hello daha basit görünümü.

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

Tıklatın **Gelişmiş Görünüm** Gelişmiş daha görünümü toosee hello varsayılan ACL'leri, maskesi ve süper kullanıcı hello kavramlarını burada gösterilir.

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a>Merhaba süper kullanıcı

Süper kullanıcı hello hello Data Lake Store tüm hello kullanıcıların çoğu haklara sahip olur. Süper kullanıcı:

* Çok RWX izinlerine sahip**tüm** dosyalar ve klasörler.
* Herhangi bir dosya veya klasör Hello izinleri değiştirebilirsiniz.
* Sahibi olan kullanıcı veya grubu herhangi bir dosya veya klasör hello değiştirebilirsiniz.

Azure’da bir Data Lake Store hesabının birkaç Azure rolü vardır, bunlar:

* Sahipler
* Katkıda Bulunanlar
* Okuyucular

Herkesin hello **sahipleri** bir Data Lake Store hesabı rolüdür otomatik olarak bu hesap için süper kullanıcı. toolearn daha, fazla [rol tabanlı erişim denetimi](../active-directory/role-based-access-control-configure.md).
Toocreate süper kullanıcı izinlerine sahip bir özel rol tabanlı erişim denetimi (RBAC) rolüne istiyorsanız, aşağıdaki izinleri toohave hello gerekir:
- Microsoft.DataLakeStore/accounts/Superuser/action
- Microsoft.Authorization/roleAssignments/write


## <a name="hello-owning-user"></a>Merhaba sahibi olan kullanıcı

Merhaba öğesini oluşturan hello otomatik olarak kullanıcı hello öğesinin sahibi olan hello kullanıcıdır. Sahip olan kullanıcı şunları yapabilir:

* Ait bir dosyanın Hello izinleri değiştirin.
* Merhaba sahibi olan kullanıcı da hello hedef grubunun bir üyesi olduğu sürece aitse, bir dosya grubunun sahibi olan hello değiştirin.

> [!NOTE]
> sahibi olan kullanıcı hello *olamaz* sahibi olan kullanıcı başka bir ait dosyasının hello değiştirin. Yalnızca süper kullanıcılar, kullanıcı bir dosyanın veya klasörün sahibi olan hello değiştirebilirsiniz.
>
>

## <a name="hello-owning-group"></a>Merhaba sahibi olan Grup

Hello POSIX ACL'leri, her kullanıcı bir "birincil grubuyla." ilişkilendirildiği Örneğin, kullanıcı "alice" toohello "Finans" grubuna ait olabilir. Alice toomultiple grupları ait olabilir, ancak bir grup her zaman kendi birincil grup olarak atanır. Bir dosya Alice oluşturduğunda, POSIX içinde bu durumda "Finans.", tooher birincil grubu bu dosya grubu hello ayarlanmış

Yeni bir dosya sistemi öğesi oluşturulduğunda, Data Lake Store Grup sahibi olan bir değer toohello atar.

* **Durum 1**: hello kök klasörü "/". Bir Data Lake Store hesabı oluşturulduğunda bu klasör oluşturulur. Bu durumda, hello sahibi olan Grup hello hesap oluşturan toohello kullanıcı ayarlanır.
* **Durum 2** (her diğer harf): yeni bir öğe oluşturulduğunda hello sahibi olan Grup hello üst klasörden kopyalanır.

Hello sahibi olan grup tarafından değiştirilebilen:
* Herhangi bir süper kullanıcı.
* Merhaba Hello sahibi olan kullanıcı aynı zamanda hello hedef grubunun bir üyesi ise kullanıcı yapamaz.

## <a name="access-check-algorithm"></a>Erişim denetimi algoritması

Aşağıdaki çizimde hello hello erişim denetimi algoritması için Data Lake Store hesaplarını temsil eder.

![Data Lake Store ACL’leri algoritması](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a>Merhaba maskesi ve "etkili izinleri"

Merhaba **maskesi** bir RWX olan değer için kullanılan toolimit erişim **kullanıcı adlı**, hello **grubu**, ve **grupları adlı** olduğunuzda Merhaba erişim denetimi algoritması gerçekleştiriliyor. Merhaba hello maskesi için temel kavramları şunlardır.

* "yürürlükte olan izinlerini." Merhaba maskesi oluşturur Diğer bir deyişle, erişim denetimi hello aynı anda hello izinlerini değiştirir.
* Merhaba maskesi doğrudan hello dosya sahibine ve Süper kullanıcılar tarafından düzenlenebilir.
* Merhaba maskesi izinleri toocreate hello etkili izni kaldırabilirsiniz. Merhaba maskesi *olamaz* izinleri toohello etkili izni ekleyin.

Bazı örneklere bakalım. Aşağıdaki örneğine hello hello maskesi çok ayarlanır**RWX**, o hello maskesi başka bir deyişle, tüm izinleri kaldırmaz. Merhaba adlı grubu ve grubun adlı kullanıcının hello yürürlükte olan izinlerini hello erişim denetimi sırasında değiştirilmediğini değil.

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

Aşağıdaki örneğine hello hello maskesi çok ayarlanır**R-X**. Bu şekilde gelir **hello yazma izinleri devre dışı bırakır** için **adlı kullanıcının**, **grubu**, ve **Grup adlı** hello zaman erişim denetleyin.

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

Başvuru için İşte bir dosya veya klasör için hello maskesi hello Azure portalında göründüğü.

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> Yeni bir Data Lake Store hesabı, hello erişim ACL hello maskesini ve varsayılan ACL hello kök için tooRWX klasörü ("/") varsayılan olarak ayarlanır.
>
>

## <a name="permissions-on-new-files-and-folders"></a>Yeni dosyalar ve klasörler üzerindeki izinler

Yeni bir dosya veya klasörün altında varolan bir klasörü oluşturulduğunda hello hello üst klasörü üzerinde ACL varsayılan belirler:

- Bir alt klasörün Varsayılan ACL’si ve Erişim ACL’si.
- Bir alt dosyanın Erişim ACL’si (dosyaları Varsayılan ACL’ye sahip değildir).

### <a name="hello-access-acl-of-a-child-file-or-folder"></a>Merhaba bir alt dosya veya klasöre erişim ACL

Bir alt dosya veya klasör oluşturulduğunda, hello üst öğenin varsayılan ACL hello alt dosya veya klasör erişim ACL hello kopyalanır. Ayrıca, varsa **diğer** kullanıcı hello üst öğenin varsayılan ACL RWX izinlere sahip, hello alt öğesi'nin erişim ACL'den kaldırılır.

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

Çoğu senaryoda, hello önceki tüm alt öğenin erişim ACL belirleme hakkında tooknow ihtiyacınız bilgilerdir. POSIX sistemleri ve istediğiniz toounderstand ayrıntılı bu dönüşüm nasıl gerçekleştirilir bilginiz varsa, ancak hello bölümüne bakın [yeni dosyalar ve klasörler için erişim ACL hello oluşturma Umask'ın rol](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) bu makalenin ilerisinde yer.


### <a name="a-child-folders-default-acl"></a>Bir alt klasörün Varsayılan ACL’si

Üst klasörü altında bir alt klasör oluşturulduğunda, toohello alt klasörün varsayılan ACL olduğu gibi hello üst klasörün varsayılan ACL üzerinden kopyalanır.

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a>Data Lake Store’da ACL’leri anlamaya yönelik gelişmiş konular

Data Lake Store dosya ve klasörler için ACL'ler nasıl belirlendiğini anlamak bazı gelişmiş konular toohelp aşağıda verilmiştir.

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a>Umask'ın rol hello erişim ACL yeni dosyalar ve klasörler için oluşturma

POSIX uyumlu bir sistemde hello genel kavram, umask tootransform hello izni için kullandığı hello üst klasörde 9-bitlik bir değer olup **sahibi olan kullanıcı**, **grubu**, ve  **diğer** hello erişim ACL yeni alt dosya veya klasör üzerinde. bir umask Hello bitleri hangi BITS tooturn hello alt öğesi'nin erişim ACL'de kapalı tanımlayın. Bu nedenle kullanılır tooselectively önlemek için izinleri hello yayılmasını **sahibi olan kullanıcı**, **grubu**, ve **diğer**.

Bir HDFS sisteminde hello umask genellikle yöneticiler tarafından denetlenen bir sitewide yapılandırma seçenektir. Data Lake Store değiştirilemeyen bir **hesap genelinde umask** kullanır. Aşağıdaki tablo gösterir hello hello için Data Lake Store maskesini kaldırın.

| Kullanıcı grubu  | Ayar | Yeni alt öğenin Erişim ACL’si üzerindeki etkisi |
|------------ |---------|---------------------------------------|
| Sahip olan kullanıcı | ---     | Etki yok                             |
| Sahip olan grup| ---     | Etki yok                             |
| Diğer       | RWX     | Okuma + Yazma + Yürütme iznini kaldırma         |

Aşağıdaki çizimde hello bu umask eylemde gösterir. Merhaba net etkisidir tooremove **okuma + yazma + yürütme** için **diğer** kullanıcı. Merhaba umask BITS belirtmediğinden **sahibi olan kullanıcı** ve **grubu**, bu izinleri olmayan dönüştürülür.

![Data Lake Store ACL’leri](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a>Merhaba Yapışkan bit

Merhaba Yapışkan bit POSIX dosya sistemi, daha gelişmiş bir özelliktir. Data Lake Store Hello bağlamında bu hello Yapışkan bit gerekli düşüktür.

Merhaba aşağıdaki tabloda hello Yapışkan bit Data Lake Store içinde nasıl çalıştığı gösterilmektedir.

| Kullanıcı grubu         | Dosya    | Klasör |
|--------------------|---------|-------------------------|
| Yapışkan bit **Kapalı** | Etki yok   | Etki yok.           |
| Yapışkan bit **Açık**  | Etki yok   | Herkes dışında engeller **Süper kullanıcılar** ve hello **sahibi olan kullanıcı** bir alt öğenin silmesini ve o alt öğesi yeniden adlandırılıyor.               |

Merhaba Yapışkan bit hello Azure portalında gösterilmez.

## <a name="common-questions-about-acls-in-data-lake-store"></a>Data Lake Store’daki ACL’ler hakkında sık sorulan sorular

Data Lake Store’daki ACL’lerle ilgili olarak sık sorulan bazı sorular aşağıda verilmiştir.

### <a name="do-i-have-tooenable-support-for-acls"></a>ACL tooenable desteği var mı?

Hayır. ACL’ler üzerinden erişim denetimi Data Lake Store hesabı için her zaman açıktır.

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a>Hangi izinlerin gerekli toorecursively delete klasörü ve içeriği misiniz?

* Merhaba üst klasörü olmalıdır **yazma + yürütme** izinleri.
* Silinen klasör toobe hello ve her bir klasörde gerektirir **okuma + yazma + yürütme** izinleri.

> [!NOTE]
> Klasörlerde toodelete dosyaları yazma izinleri gerekmez. Ayrıca, hello kök klasörü "/" için **hiçbir zaman** silinecektir.
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a>Bir dosya veya klasör hello sahibi kim?

bir dosya veya klasör Hello oluşturan hello sahibi olur.

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a>Hangi Grup, bir dosyanın veya klasörün oluşturmada grubu hello olarak ayarlanır?

Merhaba sahibi olan Grup hello üst klasörünün altında hangi hello yeni dosya veya klasör oluşturulur grubu hello kopyalanır.

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a>Sahibi olan kullanıcı dosyasının hello ben ama ihtiyacım hello RWX izinleri yok. Ne yapmalıyım?

Merhaba sahibi olan kullanıcı hello dosya toogive hello izinlerini kendilerini ihtiyaç duydukları tüm RWX izinleri değiştirebilirsiniz.

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a>ACL'ler baktığınızda hello Azure portalı kullanıcı adları görüyorum ancak GUID, görüyorum API'leri aracılığıyla neden?

Merhaba ACL girişleri toousers Azure AD içinde karşılık gelen GUID olarak depolanır. Merhaba API'leri olduğu gibi hello GUID'ler döndür. Hello Azure portal toomake ACL'ler daha kolay toouse kolay adlar mümkün olduğunda içine çevirme hello GUID'ler ile çalışır.

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a>Hello Azure portalı kullanırken neden bazen hello ACL'lerinde GUID'ler görüyorum?

Merhaba kullanıcı artık Azure AD'de mevcut olmayan bir GUID gösterilir. Genellikle bu hello kullanıcı hello şirket bırakıldığına veya hesaplarında Azure AD'de silinmiş olması durumunda gerçekleşir.

### <a name="does-data-lake-store-support-inheritance-of-acls"></a>Data Lake Store ACL’lerin devralınmasını destekler mi?

Hayır.

### <a name="what-is-hello-difference-between-mask-and-umask"></a>Merhaba maskesi ve umask arasındaki fark nedir?

| maske | umask|
|------|------|
| Merhaba **maskesi** özelliği, her dosya ve klasör kullanılabilir. | Merhaba **umask** hello Data Lake Store hesabı bir özelliğidir. Bu nedenle hello Data Lake Store yalnızca tek bir umask yoktur.    |
| bir dosya veya klasör Hello maskesi özelliği sahibi olan kullanıcı veya bir dosya veya süper kullanıcı grubu hello tarafından değiştirilebilir. | herhangi bir kullanıcı tarafından bile süper kullanıcı Hello umask özelliği değiştirilemez. Bu özellik, değiştirilemeyen sabit bir değerdir.|
| bir kullanıcı işlemi bir dosya veya klasör üzerinde hello sağ tooperform olup hello maskesi özelliği hello erişim denetimi algoritması çalışma zamanı toodetermine adresindeki sırasında kullanılır. Merhaba hello maskesi toocreate "etkili izinleri" Merhaba erişim denetimi anda rolüdür. | Merhaba umask erişim denetimi sırasında hiç kullanılmaz. Merhaba umask kullanılan toodetermine hello erişim ACL bir klasörün yeni alt öğelerinin ' dir. |
| Merhaba maskesi toonamed kullanıcı, adlandırılmış grup ve sahibi olan kullanıcı erişim denetimi hello aynı anda uygulayan bir 3-bit'lik RWX değerdir.| Merhaba umask toohello sorumlu grubu, kullanıcı, geçerli bir 9 bit değerdir ve **diğer** yeni bir alt.|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a>POSIX erişim denetimi modeli hakkında daha fazla bilgiyi nereden bulabilirim?

* [Linux üzerinde POSIX Erişim Denetim Listeleri](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [HDFS izin kılavuzu](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [POSIX SSS](http://www.opengroup.org/austin/papers/posix_faq.html)

* [POSIX 1003.1 2008](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [POSIX 1003.1 2013](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [POSIX 1003.1 2016](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [Ubuntu üzerinde POSIX ACL](https://help.ubuntu.com/community/FilePermissionsACLs)

* [Linux üzerinde erişim denetim listelerini kullanan ACL](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a>Ayrıca bkz.

* [Azure Data Lake Store'a Genel Bakış](data-lake-store-overview.md)
