---
title: "aaaHow toouse hello Android için Azure Mobile Apps SDK | Microsoft Docs"
description: "Nasıl toouse hello Azure Mobile Apps SDK'sı Android için"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a>Nasıl toouse hello Azure Mobile Apps SDK'sı Android için

Bu kılavuz size nasıl toouse hello Mobile Apps tooimplement ortak senaryolar için Android istemci SDK gibi gösterir:

* Verileri (ekleme, güncelleştirme ve silme) sorgulama.
* Kimlik doğrulaması.
* Hataları işleme.
* Merhaba istemci özelleştirme.

Bu kılavuz hello istemci tarafında Android SDK odaklanmıştır.  toolearn hakkında daha fazla bilgi mobil uygulamaları için sunucu tarafı SDK'ları Merhaba, bkz: [iş .NET arka SDK] [ 10] veya [nasıl toouse hello Node.js arka ucu SDK] [ 11].

## <a name="reference-documentation"></a>Başvuru belgeleri

Merhaba bulabilirsiniz [Javadocs API Başvurusu] [ 12] github'da hello Android istemci kitaplığı.

## <a name="supported-platforms"></a>Desteklenen platformlar

Merhaba Android için Azure Mobile Apps SDK telefon ve tablet form faktörleri için API düzey 19 24 (KitKat Nougat aracılığıyla) aracılığıyla destekler.  Kimlik doğrulaması, özellikle, bir ortak web framework yaklaşım toogather kimlik kullanır.  Sunucu akış kimlik doğrulaması saatlerde gibi küçük form faktörü cihazlarla çalışmaz.

## <a name="setup-and-prerequisites"></a>Kurulum ve Önkoşullar

Tam hello [Mobile Apps quickstart](app-service-mobile-android-get-started.md) Öğreticisi.  Bu görev, Azure Mobile Apps geliştirmek için tüm ön koşulların yerine sağlar.  Hello hızlı başlangıç ayrıca hesabınızı yapılandırma ve ilk mobil uygulama arka oluşturmanıza yardımcı olur.

Değil toocomplete hello hızlı başlangıç Öğreticisi karar verirseniz, hello aşağıdaki görevleri tamamlayın:

* [bir mobil uygulama arka ucu oluşturma] [ 13] toouse Android uygulamanızı ile.
* Android Studio'da [güncelleştirme hello Gradle derleme dosyalarını](#gradle-build).
* [Internet izni etkinleştirmek](#enable-internet).

### <a name="gradle-build"></a>Güncelleştirme hello Gradle derleme dosyası

Her ikisi de değiştirme **build.gradle** dosyaları:

1. Bu kod toohello ekleme *proje* düzeyi **build.gradle** hello içindeki dosyanın *buildscript* etiketi:

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. Bu kod toohello ekleme *modülü uygulama* düzeyi **build.gradle** hello içindeki dosyanın *bağımlılıkları* etiketi:

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    Şu anda hello son 3.3.0 sürümüdür. Merhaba desteklenen sürümleri listelenir [bintray'deki üzerinde][14].

### <a name="enable-internet"></a>Internet izin etkinleştir

tooaccess Azure, uygulamanızın etkin hello Internet izninizin olması gerekir. Zaten etkinleştirilmişse, kod tooyour satırının aşağıdaki hello eklemek **AndroidManifest.xml** dosyası:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a>İstemci bağlantısı oluşturma

Azure Mobile Apps tooyour mobil uygulama dört işlevleri sağlar:

* Veri erişimi ve bir Azure mobil uygulamalar hizmeti ile çevrimdışı eşitleme.
* Özel hello Azure mobil uygulamalar sunucusu SDK'sı ile yazılmış API'leri çağırın.
* Azure uygulama hizmeti kimlik doğrulama ve yetkilendirme ile kimlik doğrulaması.
* Anında iletme bildirimi kaydı Notification Hubs ile.

Bu işlevlerin her biri ilk oluşturduğunuz gerektiren bir `MobileServiceClient` nesnesi.  Yalnızca bir `MobileServiceClient` nesne içinde mobil istemci oluşturulmalıdır (diğer bir deyişle, bir Singleton deseni olmalıdır).  toocreate bir `MobileServiceClient` nesnesi:

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

Merhaba `<MobileAppUrl>` bir dize ya da tooyour mobil arka uç noktaları bir URL nesnesi.  Azure uygulama hizmeti toohost mobil arka kullanıyorsanız, kullandığınız hello güvenli olduğundan emin olun `https://` hello URL sürümü.

Merhaba istemci de gerektirir erişim toohello etkinlik veya Context - hello `this` hello örnekte parametresi.  Merhaba MobileServiceClient yapım hello içinde gerçekleştirileceği `onCreate()` etkinlik başvurulan hello hello yöntemi `AndroidManifest.xml` dosya.

En iyi uygulama, sunucu iletişimi kendi (singleton deseni) sınıfına soyut.  Bu durumda, geçirmelisiniz hello etkinlik hello Oluşturucusu tooappropriately içinde hello hizmeti yapılandırın.  Örneğin:

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

Şimdi Ara `AzureServiceAdapter.Initialize(this);` hello içinde `onCreate()` ana etkinlik yöntemi.  Erişim toohello istemcisi gerektiren herhangi bir yöntem kullanmak `AzureServiceAdapter.getInstance();` tooobtain başvuru toohello hizmet bağdaştırıcısı.

## <a name="data-operations"></a>Veri işlemleri

Merhaba çekirdeği hello Azure Mobile Apps SDK'sı, hello mobil uygulama arka uçta SQL Azure içinde depolanan tooprovide erişim toodata olur.  Kesin türü belirtilmiş sınıfları (tercih edilen) kullanarak bu verilere erişebilir veya türsüz sorgular (önerilmez).  Bu bölümün Hello toplu kesin türü belirtilmiş sınıflarını kullanma ile ilgilidir.

### <a name="define-client-data-classes"></a>İstemci veri sınıflarını tanımlamak

SQL Azure tablolardaki tooaccess verileri hello mobil uygulama arka ucu toohello tablolarda karşılık gelen istemci veri sınıflarını tanımlayın. Bu konudaki örnekler varsayar adlı bir tablo **MyDataTable**, sütunları aşağıdaki hello vardır:

* id
* Metin
* Tamamlayın

Merhaba karşılık gelen yazılan istemci-tarafı nesnenin bulunduğundan adlı bir dosyaya **MyDataTable.java**:

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

Eklediğiniz her bir alan için'Set ' yordamı yöntemleri ekleyin.  SQL Azure tablonuz daha fazla sütun içeriyorsa hello karşılık gelen alanları toothis sınıfı eklersiniz.  Örneğin, hello DTO (veri aktarımı nesne) sahip bir tamsayı öncelik sütunu ve'Set ' yordamı yöntemlerinin yanı sıra bu alanı ekleyebilirsiniz:

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

toocreate ek, Mobile Apps arka uç tablolarda nasıl görürüm toolearn [nasıl yapılır: bir tablo denetleyicisi tanımlamak] [ 15] (.NET arka ucu) veya [dinamik bir şema kullanarak tabloları tanımlayın] [ 16] (Node.js arka ucu).

Bir Azure Mobile Apps arka uç tablosu dört biri kullanılabilir tooclients beş özel alanları, tanımlar:

* `String id`: Merhaba hello kaydı için genel benzersiz kimliği.  En iyi uygulama, hello kimliği hello dize gösterimini yapmak bir [UUID] [ 17] nesnesi.
* `DateTimeOffset updatedAt`: hello son güncelleştirme tarihi/saati hello.  Merhaba updatedAt alan hello sunucu tarafından ayarlanır ve istemci kodunuz tarafından hiçbir zaman ayarlamanız gerekir.
* `DateTimeOffset createdAt`: hello tarih hello nesne oluşturuldu.  Merhaba createdAt alan hello sunucu tarafından ayarlanır ve istemci kodunuz tarafından hiçbir zaman ayarlamanız gerekir.
* `byte[] version`: Normal olarak bir dize olarak gösterilen, hello sürüm hello sunucu tarafından ayarlanır.
* `boolean deleted`: Hello kayıt silindi ancak henüz temizlendi değil olduğunu gösterir.  Kullanmayın `deleted` sınıfınız özelliği olarak.

Merhaba `id` alan gereklidir.  Merhaba `updatedAt` alan ve `version` alan çevrimdışı eşitleme için kullanılan (Artımlı eşitleme ve Çakışma çözümlemesi için sırasıyla).  Merhaba `createdAt` alan başvurusu alan ve hello istemci tarafından kullanılmaz.  Merhaba adları "arasında hat" Merhaba özellik adlarını ve ayarlanabilir değil.  Ancak, nesne ve hello arasında bir eşleme hello kullanarak "arasında hat" adları oluşturabilirsiniz [gson] [ 3] kitaplığı.  Örneğin:

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a>Bir tablo başvurusu oluşturma

ilk tooaccess bir tablo oluşturun bir [MobileServiceTable] [ 8] arama hello nesnesiyle **getTable** hello yöntemi [MobileServiceClient][9].  Bu yöntem iki aşırı yüklemeye sahip:

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

Kod, aşağıdaki hello içinde **mClient** bir başvuru tooyour MobileServiceClient nesnesidir.  Hello ilk aşırı hello sınıf adı ve hello tablo adı aynı hello ve hello hello hızlı başlangıç kullanılır nerede kullanılır:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

Merhaba tablo adı hello sınıfı adından farklı olduğunda hello ikinci aşırı kullanılır: hello ilk parametredir hello tablo adı.

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <a name="query"></a>Arka uç tablosu sorgulama

İlk olarak, bir tablo başvurusu edinin.  Ardından hello tablo başvurusu üzerinde bir sorgu yürütün.  Bir sorgu herhangi bir bileşimini şöyledir:

* A `.where()` [filtre yan tümcesi](#filtering).
* Bir `.orderBy()` [yan tümcesinin sıralama](#sorting).
* A `.select()` [alan seçimi yan tümcesi](#selection).
* A `.skip()` ve `.top()` için [sonuçları disk belleği](#paging).

Merhaba yan tümceleri sipariş önceki hello sunulmalıdır.

### <a name="filter"></a>Sonuçları filtreleme

Merhaba genel bir sorgu şu şekildedir:

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

Merhaba önceki örnekte tüm sonuçları (yukarı toohello en fazla sayfa boyutu hello sunucu tarafından ayarını) döndürür.  Merhaba `.execute()` yöntemi hello arka uçta hello sorgu yürütür.  Merhaba dönüştürülmüş tooan sorgudur [OData v3] [ 19] iletim toohello Mobile Apps arka önce sorgu.  Giriş üzerinde hello Mobile Apps arka hello sorgu hello SQL Azure örneğinde yürütmeden önce bir SQL deyimi dönüştürür.  Ağ etkinliği biraz zaman alır beri hello `.execute()` yöntemi döndürür bir [ `ListenableFuture<E>` ] [ 18].

### <a name="filtering"></a>Döndürülen veri filtreleme

sorgu yürütme aşağıdaki hello hello tüm öğeleri döndürür **Todoıtem** tablo nerede **tam** eşittir **false**.

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

**mToDoTable** daha önce oluşturduğumuz hello başvuru toohello mobil hizmeti tablo.

Hello kullanarak bir filtre tanımlar **burada** hello tablo başvurusu üzerinde yöntem çağrısı. Merhaba **nerede** yöntemi tarafından izlenen bir **alan** yöntemi ve ardından bir yöntemle hello mantıksal koşulu belirtir. Olası koşul yöntemleri dahil **eq** (eşittir) **ne** (eşit değildir), **gt** (büyük), **ge** (büyük veya eşittir) **lt** (küçüktür), **le** (küçük veya eşittir). Bu yöntemler numarası karşılaştırmanıza olanak tanır ve toospecific değerleri dize alanları.

Tarihleri filtreleyebilirsiniz. Merhaba aşağıdaki yöntemlerden hello tüm tarih alanı veya hello tarih kısımlarını karşılaştırmanıza olanak tanır: **yıl**, **ay**, **gün**, **saat**, **minute**, ve **ikinci**. Merhaba aşağıdaki örnek, öğe için bir filtre, *son tarih* 2013'e eşittir.

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

Merhaba aşağıdaki yöntemlerden karmaşık filtreler dize alanları destekler: **startsWith**, **endsWith**, **concat**, **subString**, **indexOf**, **Değiştir**, **toLower**, **toUpper**, **kırpma**, ve  **Uzunluk**. Merhaba burada tablo satır için örnek filtreleri aşağıdaki hello *metin* sütun "PRI0" ile başlar

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

işleç yöntemler aşağıdaki hello numara alanları desteklenir: **ekleme**, **alt**, **mul**, **div**, **mod**, **kat**, **tavan**, ve **yuvarlak**. Merhaba burada tablo satır için örnek filtreleri aşağıdaki hello **süresi** bir çift sayı.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

Bu mantıksal yöntemlerle koşulları birleştirebilirsiniz: **ve**, **veya** ve **değil**. Aşağıdaki örnek hello iki örnekler önceki hello birleştirir.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

Mantıksal işleçler: Grup ve iç içe geçirme

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

Daha ayrıntılı tartışma ve filtreleme örnekleri için bkz: [hello Android istemci sorgu modelini hello zenginliğinin keşfetme][20].

### <a name="sorting"></a>Döndürülen veriler sıralama

Merhaba aşağıdaki kod tüm öğeleri bir tablodan döndürür **Todoıtems** hello göre artan *metin* alan. *mToDoTable* daha önce oluşturduğunuz hello başvuru toohello arka uç tablosu:

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

Merhaba öğesinin ilk parametresi, hello **orderBy** yöntemi hangi toosort hello alanının bir dize eşit toohello adıdır. Merhaba ikinci parametre kullanan hello **QueryOrder** numaralandırma toospecify olup olmadığını artan veya azalan toosort.  Hello kullanarak filtre ***nerede*** yöntemi, hello ***nerede*** önce hello yöntemi çağrıldıktan ***orderBy*** yöntemi.

### <a name="selection"></a>Belirli sütunları seçin

Merhaba aşağıdaki kod bir tablodan nasıl tooreturn tüm öğeleri gösterir **Todoıtems**, ancak yalnızca, hello görüntüler **tam** ve **metin** alanları. **mToDoTable** daha önce oluşturduğumuz hello başvuru toohello arka uç tablo.

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

Merhaba parametreleri toohello select işlevi tooreturn istediğiniz Merhaba tablonun sütunlarının hello dize adları var.  Merhaba **seçin** yönteminin gerekir toofollow yöntemler gibi **nerede** ve **orderBy**. Disk belleği yöntemler gibi tarafından izlenebilir **atla** ve **üst**.

### <a name="paging"></a>Dönüş verileri sayfalarında

Veri **her zaman** sayfalarında döndürdü.  Merhaba en fazla döndürülen kayıt sayısını hello sunucu tarafından ayarlanır.  Daha fazla kayıt Hello istemci isteklerini varsa hello sunucu hello en fazla kayıt sayısı değerini döndürür.  Varsayılan olarak, hello sunucuda hello en büyük sayfa boyutu 50 kayıttır.

Merhaba ilk örneği, nasıl tooselect hello bir tablodan en üstteki beş öğelerini gösterir. Merhaba sorgunun döndürdüğü hello öğeleri bir tablodan **Todoıtems**. **mToDoTable** daha önce oluşturduğunuz hello başvuru toohello arka uç tablosu:

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

İlk beş öğeleri atlar hello ve ardından sonraki beş döndürür hello bir sorgu şöyledir:

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

Bir tablodaki tüm kayıtları tooget isterseniz, kod tooiterate tüm sayfalar kullanın:

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

Bir istek bu yöntemi kullanarak tüm kayıtlar için en az iki isteği toohello Mobile Apps arka oluşturur.

> [!TIP]
> Seçme hello sağ sayfa hello isteği sürerken bellek kullanımı, bant genişliği kullanımı ve hello veri tamamen alma gecikme arasında bir denge boyutudur.  Merhaba varsayılan (50 kayıtları) tüm aygıtlar için uygundur.  Özellikle büyük bellek cihazlarda çalışmazsa, too500 artırın.  500 sonuçlarını kaydeder, artan hello sayfa boyutu kabul edilebilir gecikme ve büyük bellek sorunları bulunan.

### <a name="chaining"></a>Nasıl yapılır: Sorgu yöntemleri birleştirme

arka uç tabloları sorgulama kullanılan hello yöntemler art arda eklenmiş. Zincirleme sorgu yöntemleri tooselect belirli sütunlardaki sıralanır ve disk belleği filtrelenmiş satır sağlar. Karmaşık mantıksal filtreler oluşturabilirsiniz.  Her sorgu yöntemi, bir sorgu nesnesi döndürür. tooend hello dizi yöntem ve gerçekte çalışma hello sorgu, çağrı hello **yürütme** yöntemi. Örneğin:

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

Merhaba yöntemleri şöyle sıralanmalıdır sorgu zincirleme:

1. Filtreleme (**burada**) yöntemleri.
2. Sıralama (**orderBy**) yöntemleri.
3. Seçim (**seçin**) yöntemleri.
4. disk belleği (**atla** ve **üst**) yöntemleri.

## <a name="binding"></a>Veri toohello kullanıcı arabirimi bağlama

Veri bağlama üç bileşenleri içerir:

* Merhaba veri kaynağı
* Başlangıç ekranı düzeni
* Merhaba bağdaştırıcısı TIES iki birlikte hello olduğunu.

Bizim örnek kodda hello veri hello Mobile Apps SQL Azure tablosundan döndürürüz **Todoıtem** bir dizi içine. Veri uygulamaları için genel bir desen etkinliktir.  Veritabanı sorguları genellikle bir liste veya dizideki istemci alır hello satır koleksiyonu döndürür. Bu örnekte, hello dizi hello veri kaynağıdır.  Merhaba kod hello aygıtta görünür hello verilerinin hello görünümü tanımlayan bir ekran düzenini belirtir.  Merhaba iki hello uzantısıdır, bu kodda bir bağdaştırıcı ile birlikte bağlı **ArrayAdapter&lt;Todoıtem&gt;**  sınıfı.

#### <a name="layout"></a>Merhaba düzeni tanımlayın

Merhaba düzeni birkaç XML kodu parçacıkları tarafından tanımlanır. Varolan bir düzeni verilen, koddan hello hello temsil **ListView** sunucusunu verilerimizi toopopulate istiyoruz.

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

Kod önceki hello hello *LISTITEM* özniteliği hello listesinde tek bir satır için hello düzeni hello kimliğini belirtir. Bu kod bir onay kutusu ve ilgili metin belirtir ve hello listesindeki her bir öğe için bir kez örneği. Bu düzen hello görüntülemez **kimliği** alan ve daha karmaşık bir düzen belirtirsiniz ek alanlar hello görüntüleme. Bu kodu hello **row_list_to_do.xml** dosya.

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <a name="adapter"></a>Merhaba bağdaştırıcısı tanımlayın
Bizim görünümünün Hello veri kaynağı bir dizi olduğundan **Todoıtem**, biz alt bizim bağdaştırıcısından bir **ArrayAdapter&lt;Todoıtem&gt;**  sınıfı. Bu alt sınıf için bir görünüm üreten her **Todoıtem** hello kullanarak **row_list_to_do** düzeni.  Bizim kodda hello uzantısıdır sınıfı aşağıdaki hello tanımlarız **ArrayAdapter&lt;E&gt;**  sınıfı:

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

Merhaba bağdaştırıcıları geçersiz kılma **getView** yöntemi. Örneğin:

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

Biz bu sınıfının bir örneği bizim etkinliğinde gibi oluşturun:

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

Merhaba ikinci parametre toohello ToDoItemAdapter Oluşturucusu bir başvuru toohello düzeni ' dir. Biz şimdi hello örneğini oluşturabilirsiniz **ListView** ve hello bağdaştırıcısı toohello Ata **ListView**.

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <a name="use-adapter"></a>Merhaba bağdaştırıcısı tooBind toohello UI kullanın

Hazır toouse veri bağlama sunulmuştur. Merhaba aşağıdaki kod tooget öğeler hello tablo ve dolgular yerel bağdaştırıcı öğeleri döndürülen hello ile nasıl hello gösterir.

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

Merhaba bağdaştırıcısı hello değiştirmek istediğiniz zaman arama **Todoıtem** tablo. Bir kayıt kayıt temelinde yapılır ve değişiklikleri olduğundan, bir koleksiyon yerine tek bir satır işleyici. Bir öğe eklediğinizde, hello çağrısı **eklemek** yöntemi üzerinde hello bağdaştırıcısı; silerken hello çağrısı **kaldırmak** yöntemi.

Hello tam bir örnek bulabilirsiniz [Android hızlı başlangıç projesi][21].

## <a name="inserting"></a>Hello arka uç veri Ekle

Merhaba bir örneği *Todoıtem* sınıfını ve özelliklerini ayarlayın.

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

Ardından **INSERT()** tooinsert nesneyi:

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

Merhaba hello arka uç tablo, dahil edilen hello kimliği ve diğer tüm değerler eklenen hello veri varlığı eşleşme döndürdü (Merhaba gibi `createdAt`, `updatedAt`, ve `version` alanları) hello arka uçta ayarlayın.

Mobile Apps tabloları gerektiren adlı birincil anahtar sütunu **kimliği**. Bu sütun bir dize olmalıdır. Merhaba kimliği sütunun Hello varsayılan değeri bir GUID değeridir.  E-posta adresleri veya kullanıcı adları gibi diğer benzersiz değerler sağlayabilirsiniz. Bir dize kimliği değeri için eklenen bir kaydı sağlanmadığında hello arka uç yeni bir GUID oluşturur.

Dize kimliği değerleri hello aşağıdaki avantajları sağlar:

* Gidiş dönüş toohello veritabanı yapmadan kimlikleri oluşturulabilir.
* Farklı tablolar veya veritabanlarına daha kolay toomerge kayıtlarıdır.
* KOD değerleri daha iyi bir uygulama mantığı ile tümleştirin.

Dize kimliği değerler **gerekli** çevrimdışı eşitleme desteği.  Merhaba arka uç veritabanında depolandıktan sonra bir kimliğini değiştiremezsiniz.

## <a name="updating"></a>Bir mobil uygulama verileri güncelleştirme

bir tabloda tooupdate veri iletmek hello yeni nesne toohello **update()** yöntemi.

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

Bu örnekte, *öğesi* hello başvuru tooa sırada *Todoıtem* bazı yapılan değişiklikler tooit dolmadığı tablo.  Merhaba satır hello ile aynı **kimliği** güncelleştirilir.

## <a name="deleting"></a>Bir mobil uygulama verilerini sil

koddan hello nasıl toodelete veri belirterek bir tablodan veri nesnesi hello gösterir.

```java
mToDoTable
    .delete(item);
```

Merhaba belirterek öğeyi silebilirsiniz **kimliği** hello satır toodelete alanı.

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <a name="lookup"></a>Belirli bir öğeyi kimliğe göre arayın

Belirli bir sahip bir öğe aramak **kimliği** hello ile alan **lookUp()** yöntemi:

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <a name="untyped"></a>Nasıl yapılır: türsüz verilerle çalışma

Merhaba türsüz programlama modeli, JSON seri hale getirme üzerinde tam denetim sağlar.  Burada türsüz programlama modeli toouse isteyebilir bazı yaygın senaryolar vardır. Örneğin, arka uç tablonuz fazla sayıda sütun içeriyorsa ve tooreference hello bir sütun alt kümesini yeterlidir.  Merhaba yazılan modeli tüm hello sütunları hello Mobile Apps arka uç veri sınıfınızda tanımlanan toodefine gerektirir.  API çağrıları verilerine erişmek için hello çoğu benzer toohello programlama çağrıları belirtilmiş. Merhaba ana hello türsüz modelinde, hello yöntemleri çağırma farktır **MobileServiceJsonTable** hello yerine **MobileServiceTable** nesnesi.

### <a name="json_instance"></a>Türsüz tablo örneği oluşturma

Benzer toohello yazılan modeli, bir tablo başvurusu alarak başlatılır, ancak bu durumda olduğu bir **MobileServicesJsonTable** nesnesi. Merhaba başvuru tarafından arama hello elde **getTable** hello istemci örneği üzerinde yöntemi:

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

Merhaba örneği oluşturduktan sonra **MobileServiceJsonTable**, onu sahip neredeyse hello aynı API hello yazılan programlama modeli olarak kullanılabilir. Bazı durumlarda, hello yöntemleri türü belirsiz bir parametre türü belirtilmiş bir parametre yerine getirin.

### <a name="json_insert"></a>Türü belirsiz bir tabloya ekleme
kodun gösterdiği nasıl aşağıdaki hello toodo ekleme. Merhaba ilk toocreate adımdır bir [JsonObject][1], hello parçası olduğu [gson] [ 3] kitaplığı.

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

Ardından, **INSERT()** tooinsert hello türsüz nesnesine hello tablo.

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

Eklenen hello nesnesinin tooget hello kimliği gerekirse hello kullanın **getAsJsonPrimitive()** yöntemi.

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <a name="json_delete"></a>Türü belirsiz bir tablodan silin
Merhaba aşağıdaki kod nasıl toodelete bir örnek, bu durumda, hello aynı örneği gösterir bir **JsonObject** hello önceden oluşturulmuş *Ekle* örnek. Merhaba kodudur hello aynı hello olarak yazılmış durumda, ancak hello yöntem sahip farklı bir imza başvurduğu bu yana bir **JsonObject**.

```java
mToDoTable
    .delete(insertedItem);
```

Doğrudan Kimliğini kullanarak bir örneği daha da silebilirsiniz:

```java
mToDoTable.delete(ID);
```

### <a name="json_get"></a>Türü belirsiz bir tablodan tüm satırları döndürür
kodun gösterdiği nasıl aşağıdaki hello tooretrieve tüm bir tabloyu. Bir JSON tablo kullandığından, seçmeli olarak yalnızca bazı Merhaba tablonun sütunlarının alabilirsiniz.

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

Merhaba filtreleme, filtreleme ve disk belleği'hello yazılan model için kullanılabilir yöntemleri aynı kümesini hello türsüz model için kullanılabilir.

## <a name="offline-sync"></a>Çevrimdışı eşitleme uygulama

Hello Azure Mobile Apps istemci SDK'sı bir SQLite veritabanı toostore hello sunucu verilerin bir kopyasını kullanarak yerel olarak çevrimdışı veri eşitlemeyi de uygular.  Çevrimdışı bir tablo üzerinde gerçekleştirilen işlemler mobil bağlantı toowork gerektirmez.  Çevrimdışı eşitleme yardımları esnekliği ve çakışma çözümü için daha karmaşık mantığı hello gider performans.  Hello Azure Mobile Apps istemci SDK'sı özellikler aşağıdaki hello uygular:

* Artımlı eşitleme: Bant genişliği ve bellek tüketimi kaydetme yalnızca güncelleştirilmiş ve yeni kayıtlar indirilir.
* İyimser eşzamanlılık: İşlemleri toosucceed varsayılır.  Çakışma çözümü, güncelleştirmelerinin hello sunucuda gerçekleştirilir kadar ertelenir.
* Çakışma çözümü: çakışan değişikliği hello sunucuda yapılan ve SDK algılar hello tooalert hello kullanıcı kanca oluşturur.
* Geçici silme: Silinen kayıtlar, diğer aygıtlar tooupdate çevrimdışı önbelleklerini izin vererek, silinen işaretlenir.

### <a name="initialize-offline-sync"></a>Çevrimdışı eşitleme başlatılamadı

Çevrimdışı her tablo hello Çevrimdışı Önbellek kullanmadan önce tanımlanması gerekir.  Normalde, tablo tanımı hemen hello istemcisinin hello oluşturulduktan sonra gerçekleştirilir:

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a>Başvuru toohello çevrimdışı önbellek tablosunu alın

Çevrimiçi bir tablo için kullandığınız `.getTable()`.  Çevrimdışı bir tablo için kullanın `.getSyncTable()`:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

Tüm iş eşit çevrimiçi tabloları (filtreleme, sıralama, disk belleği, veri ekleme, verilerini güncelleştirmek ve verileri silme dahil) için kullanılabilen yöntemleri hello iyi tablolarda çevrimiçi ve çevrimdışı.

### <a name="synchronize-hello-local-offline-cache"></a>Merhaba yerel Çevrimdışı Önbellek Eşitle

Eşitleme Merhaba, uygulamanızın içinde denetimdir.  Bir örnek eşitleme yöntemi şöyledir:

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

Bir sorgu adı toohello sağladıysanız `.pull(query, queryname)` yöntemi Artımlı eşitleme olduğundan oluşturulan veya son başarıyla tamamlandı hello çekme beri değiştirilen kullanılan tooreturn yalnızca kaydeder.

### <a name="handle-conflicts-during-offline-synchronization"></a>Çevrimdışı eşitleme sırasında çakışmalarını işleme

Sırasında bir çakışma olursa bir `.push()` işlemi, bir `MobileServiceConflictException` oluşturulur.   Hello sunucusu verilen öğesi hello özel durum katıştırılır ve tarafından alınan `.getItem()` hello özel durumunda.  Merhaba MobileServiceSyncContext nesnesinde öğeleri aşağıdaki arama hello tarafından Hello itme ayarlayın:

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

İstediğiniz gibi tüm çakışmaları işaretlenmiş sonra çağrı `.push()` yeniden tooresolve tüm çakışmaları hello.

## <a name="custom-api"></a>Özel bir API çağrısı

Özel bir API değil tooan INSERT eşleme, güncelleştirme, silme veya okuma işlemi sunucusu işlevselliği kullanıma toodefine özel uç noktaları sağlar. Özel bir API kullanarak, okuma ve HTTP ileti üstbilgilerini ayarlama ve JSON dışında bir ileti gövdesinin biçimi tanımlama gibi Mesajlaşma üzerinde daha fazla denetim olabilir.

Bir Android istemciden hello çağrısı **invokeApi** yöntemi toocall hello özel API uç noktası. Merhaba aşağıdaki örnekte nasıl toocall bir API uç noktası adlı gösterir **completeAll**, adlı bir koleksiyon sınıfı döndürür **MarkAllResult**.

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

Merhaba **invokeApi** yöntemi, bir POST isteği toohello yeni özel API gönderir hello istemcide çağrılır. hataları gibi hello sonuç hello özel API tarafından döndürülen bir ileti iletişim kutusunda görüntülenmez. Diğer sürümleri **invokeApi** isteğe bağlı olarak nesneyi hello istek gövdesinde gönderme, hello HTTP yöntemini belirtin ve sorgu parametreleri hello isteği ile Gönder olanak tanır. Türsüz sürümlerini **invokeApi** de sağlanır.

## <a name="authentication"></a>Kimlik doğrulama tooyour uygulama Ekle

Öğreticiler zaten ayrıntılı olarak açıklayan nasıl tooadd bu özellikleri.

Uygulama hizmetini destekleyen [uygulama kullanıcıların kimlik doğrulaması](app-service-mobile-android-get-started-users.md) çeşitli dış kimlik sağlayıcılarını kullanarak: Facebook, Google, Microsoft Account, Twitter ve Azure Active Directory. Tooonly kimliği doğrulanmış kullanıcıların belirli işlemler için tabloları toorestrict erişim izinlerini ayarlayabilirsiniz. Arka ucunuza kimliği doğrulanmış kullanıcılar tooimplement yetkilendirme kuralları hello kimliğini de kullanabilirsiniz.

İki kimlik doğrulama akışı desteklenir: bir **server** akış ve **istemci** akış. Merhaba kimlik sağlayıcıları web arabirimine alacağından hello sunucu akış hello Basit kimlik doğrulama deneyimi sağlar.  Hiçbir ek SDK'ları gerekli tooimplement sunucu akış kimlik doğrulaması ' dir. Kimlik doğrulaması akışı hello mobil cihaz derin bir tümleştirmeye sağlamaz ve yalnızca kavram senaryoları kanıtı için önerilir.

hello kimlik sağlayıcısı tarafından sağlanan SDK'ları kullanır gibi hello istemci akışı çoklu oturum açma gibi aygıta özgü özellikleri ile daha derin tümleştirme sağlar.  Örneğin, mobil uygulamanıza hello Facebook SDK tümleştirebilirsiniz.  Merhaba mobil istemci hello Facebook uygulamaya değiştirir ve, mobil uygulama arka tooyour takas önce oturum onaylar.

Gerekli tooenable kimlik doğrulaması, uygulamanızda dört adımlardır:

* Uygulamanızın kimlik doğrulaması için bir kimlik sağlayıcısı ile kaydedin.
* Uygulama hizmeti arka yapılandırın.
* Tablo izinleri tooauthenticated kullanıcıları yalnızca hello uygulama hizmeti arka uç kısıtlayın.
* Kimlik doğrulama kodu tooyour uygulama ekleyin.

Tooonly kimliği doğrulanmış kullanıcıların belirli işlemler için tabloları toorestrict erişim izinlerini ayarlayabilirsiniz. Merhaba kimliği doğrulanmış kullanıcı toomodify SID'si de kullanabilirsiniz istekleri.  Daha fazla bilgi için gözden [kimlik doğrulamayı kullanmaya başlama] ve hello Server SDK nasıl yapılır belgeleri.

### <a name="caching"></a>Kimlik doğrulaması: Sunucu akışı

Merhaba aşağıdaki kod hello Google sağlayıcısını kullanarak bir sunucu akış oturum açma işlemi başlatır.  Ek yapılandırma hello Google sağlayıcısı için hello güvenlik gereksinimleri nedeniyle gereklidir:

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

Ayrıca, yöntem toohello ana etkinlik sınıfıyla aşağıdaki hello ekleyin:

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    // When request completes
    if (resultCode == RESULT_OK) {
        // Check hello request code matches hello one we send in hello login request
        if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
            MobileServiceActivityResult result = mClient.onActivityResult(data);
            if (result.isLoggedIn()) {
                // login succeeded
                createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                createTable();
            } else {
                // login failed, check hello error message
                String errorMessage = result.getErrorMessage();
                createAndShowDialog(errorMessage, "Error");
            }
        }
    }
}
```

Merhaba `GOOGLE_LOGIN_REQUEST_CODE` , ana tanımlanan etkinliği hello için kullanılan `login()` yöntemi ve hello içinde `onActivityResult()` yöntemi.  Merhaba aynı numarası hello içinde kullanılan sürece herhangi bir benzersiz sayı seçebilirsiniz `login()` yöntemi ve hello `onActivityResult()` yöntemi.  (Daha önce gösterildiği gibi) bir hizmet bağdaştırıcısı hello istemci kodu soyut, hello hizmet bağdaştırıcısında hello uygun yöntemleri çağırmanız gerekir.

Ayrıca tooconfigure hello proje için customtabs gerekir.  Önce bir yeniden yönlendirme URL'si belirtin.  Kod parçacığında çok aşağıdaki hello eklemek`AndroidManifest.xml`:

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

Merhaba eklemek **redirectUriScheme** toohello `build.gradle` dosya uygulamanız için:

```text
android {
    buildTypes {
        release {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
        debug {
            // … …
            manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
        }
    }
}
```

Son olarak, ekleme `com.android.support:customtabs:23.0.1` hello toohello bağımlılıkları listesinde `build.gradle` dosyası:

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

Kullanıcı oturum açma hello Hello kimliği elde bir **MobileServiceUser** hello kullanarak **getuserıd öğesini** yöntemi. Nasıl toouse vadeli toocall hello zaman uyumsuz oturum açma API'leri ilişkin bir örnek için bkz: [kimlik doğrulamayı kullanmaya başlama].

> [!WARNING]
> Merhaba URL belirtilen düzeni büyük/küçük harf duyarlıdır.  Emin tüm oluşumlarını `{url_scheme_of_you_app}` eşleşen durumda.

### <a name="caching"></a>Önbellek kimlik doğrulama belirteçleri

Kimlik doğrulama belirteçleri önbelleğe alma toostore hello kullanıcı kimliği ve kimlik doğrulama belirteci hello cihazda yerel olarak gerektirir. Merhaba hello uygulama, bir sonraki başlatılışında, hello önbellek denetleyin ve bu değerleri varsa hello günlüğüne yordamı atlayın ve bu verilerle hello istemci rehydrate. Ancak bu verileri duyarlıdır ve hello telefon çalınırsa durumda güvenliği şifrelenmiş depolanması gerekir.  İçinde nasıl toocache kimlik doğrulama belirteçleri, tam bir örnek görebilirsiniz [önbelleğe kimlik doğrulama belirteçleri bölümü][7].

Toouse süresi dolmuş bir belirteci çalıştığınızda aldığınız bir *yetkisiz 401* yanıt. Filtreleri kullanarak kimlik doğrulama hataları işleyebilir.  Filtreler istekleri toohello uygulama hizmeti arka uç kesebilir. Merhaba filtre kodu bir 401 hello yanıtı testleri, hello oturum açma işlemini tetikler ve hello 401 oluşturulan hello isteği sürdürür.

### <a name="refresh"></a>Yenileme belirteçleri kullanın

Azure App Service kimlik doğrulaması ve yetkilendirme tarafından döndürülen hello belirteci tanımlı yaşam süresi bir saat sahip.  Bu süre hello kullanıcı sağlamalarını gerekir.  Kullanıyorsanız istemci akışı kimlik doğrulaması yoluyla aldığınız ardından sağlamalarını uzun süreli bir belirteç ile Azure App Service kimlik doğrulaması kullanarak ve yetkilendirme kullanarak aynı belirteci hello.  Başka bir Azure uygulama hizmeti belirteci ile yeni bir yaşam süresi oluşturulur.

Merhaba sağlayıcısı toouse yenileme belirteçleri da kaydedebilirsiniz.  Bir yenileme belirteci her zaman kullanılabilir değil.  Ek yapılandırma gerekli değildir:

* İçin **Azure Active Directory**, gizli hello Azure Active Directory uygulaması için yapılandırın.  Merhaba istemci parolası, Azure Active Directory kimlik doğrulamasını yapılandırırken hello Azure uygulama hizmeti belirtin.  Çağrılırken `.login()`, geçirmek `response_type=code id_token` bir parametre olarak:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* İçin **Google**, hello geçirmek `access_type=offline` bir parametre olarak:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* İçin **Microsoft Account**seçin hello `wl.offline_access` kapsam.

toorefresh bir belirteç çağrı `.refreshUser()`:

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

En iyi uygulama, bir 401 yanıtına hello sunucusundan algılar ve toorefresh hello kullanıcı belirteci çalışır bir filtre oluşturun.

## <a name="log-in-with-client-flow-authentication"></a>Oturum akış olmayan istemci kimlik doğrulaması ile oturum

Merhaba akış olmayan istemci kimlik doğrulaması oturum açma için genel işlem aşağıdaki gibidir:

* Azure App Service kimlik doğrulama ve yetkilendirme akışı sunucu kimlik doğrulaması gibi yapılandırın.
* Kimlik doğrulama tooproduce bir erişim belirteci için Hello kimlik doğrulama sağlayıcısı SDK tümleştirin.
* Merhaba çağrı `.login()` yöntemini aşağıdaki şekilde:

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

Hello yerine `onSuccess()` , kod ile yöntemi başarılı oturum açma toouse istiyor.  Merhaba `{provider}` dizedir geçerli bir sağlayıcısı: **aad** (Azure Active Directory), **facebook**, **google**, **microsoftaccount**, veya **twitter**.  Özel kimlik doğrulama uyguladıysanız, hello özel kimlik doğrulama sağlayıcısı etiketi de kullanabilirsiniz.

### <a name="adal"></a>Kullanıcılar hello Active Directory Authentication Library (ADAL) ile kimlik doğrulaması

Azure Active Directory'yi kullanarak uygulamanıza hello Active Directory Authentication Library (ADAL) toosign kullanıcılar kullanabilir. Bir istemci akış oturum kullanmaktır genellikle tercih toousing hello `loginAsync()` yöntemleri olarak daha yerel bir UX fikir sağlar ve ek özelleştirme için sağlar.

1. Aşağıdaki hello tarafından mobil uygulamanızın arka ucuna AAD oturum açma için yapılandırma [tooconfigure App Service nasıl Active Directory oturum açma için] [ 22] Öğreticisi. Yerel istemci uygulaması kaydı emin toocomplete hello isteğe bağlı adım olun.
2. ADAL tanımları izleyerek, build.gradle dosya tooinclude hello değiştirerek yükleyin:

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. Aşağıdaki kod tooyour uygulama, değişiklikleri izleyen hello yapmadan hello ekleyin:

* Değiştir **INSERT yetkilisi burada** uygulamanızı sağlanan hello Kiracı hello adı. Merhaba biçiminde https://login.microsoftonline.com/contoso.onmicrosoft.com olmalıdır.
* Değiştir **Ekle-RESOURCE-kimliği-Buraya** , mobil uygulamanızın arka ucuna için hello istemci kimliği. Hello hello istemci kimliği elde edebilirsiniz **Gelişmiş** altında sekmesinde **Azure Active Directory ayarları** hello Portalı'nda.
* Değiştir **Ekle-istemci-kimliği-Buraya** hello yerel istemci uygulamasından kopyaladığınız hello istemci kimliği.
* Değiştir **Ekle-REDIRECT-URI-Buraya** sitenizin ile */.auth/login/done* hello HTTPS şeması kullanarak uç nokta. Bu değer çok benzer olmalıdır*https://contoso.azurewebsites.net/.auth/login/done*.

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <a name="filters"></a>Merhaba istemci-sunucu iletişimi Ayarla

Merhaba istemci bağlantısı normalde HTTP kitaplığı hello Android SDK ile sağlanan temel hello kullanarak temel bir HTTP bağlantısı olur.  Neden istediğiniz toochange birkaç nedeni vardır:

* Alternatif bir HTTP kitaplığı tooadjust zaman aşımları toouse istiyor.
* Bir ilerleme çubuğu tooprovide istiyor.
* Bir özel üstbilgi toosupport API management işlevselliği tooadd istiyor.
* Böylece, yeniden kimlik doğrulamanın uygulayabileceğiniz başarısız bir yanıt toointercept istiyor.
* Toolog arka uç istekleri tooan analytics hizmeti istiyor.

### <a name="using-an-alternate-http-library"></a>Alternatif bir HTTP kitaplığı kullanma

Merhaba çağrı `.setAndroidHttpClientFactory()` istemci başvurusu oluşturduktan sonra hemen yöntemi.  Örneğin, tooset hello bağlantı zaman aşımı too60 saniye (yerine hello varsayılan 10 saniye):

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a>Bir ilerleme filtre uygulama

Her istek bir kesme noktası uygulayarak uygulayabilirsiniz bir `ServiceFilter`.  Örneğin, bir önceden oluşturulmuş ilerleme çubuğu hello aşağıdaki güncelleştirmeler:

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

Bu filtre toohello istemci aşağıdaki gibi ekleyebilirsiniz:

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a>İstek üstbilgilerini özelleştirme

Merhaba aşağıdaki kullanın `ServiceFilter` ve hello hello filtresi ekleme hello aynı şekilde `ProgressFilter`:

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <a name="conversions"></a>Otomatik serileştirme yapılandırın

Hello kullanarak tooevery sütunu geçerli bir dönüştürme stratejisi belirtebilirsiniz [gson] [ 3] API. Merhaba Android istemci kitaplığını kullanan [gson] [ 3] hello veri tooAzure uygulama hizmeti gönderilmeden önce hello arka planda tooserialize Java tooJSON veri nesneleri.  Merhaba aşağıdaki kod kullanır hello **setFieldNamingStrategy()** yöntemi tooset hello stratejisi. Bu örnek hello ilk karakter ("m") ve her alan adı için ardından küçük hello sonraki karakteri siler. Örneğin, "id" "Orta" etkinleştirmeniz  Bir dönüştürme stratejisi tooreduce hello gereken uygulama `SerializedName()` çoğu alanlara ek açıklamaları.

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

Bu kod hello kullanan bir mobil istemci başvuru oluşturmadan önce yürütülmelidir **MobileServiceClient**.

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[kimlik doğrulamayı kullanmaya başlama]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
