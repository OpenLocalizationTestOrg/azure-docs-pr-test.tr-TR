---
title: "Güvenilir koleksiyonlarıyla aaaWorking | Microsoft Docs"
description: "Güvenilir koleksiyonları ile çalışmak için en iyi yöntemler hello öğrenin."
services: service-fabric
documentationcenter: .net
author: rajak
manager: timlt
editor: 
ms.assetid: 39e0cd6b-32c4-4b97-bbcf-33dad93dcad1
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/19/2017
ms.author: rajak
ms.openlocfilehash: 41ba0b257da8493c1fc2e99ad7565593dc7cbcce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-reliable-collections"></a>Güvenilir koleksiyonları ile çalışma
Service Fabric programlama modeli kullanılabilir too.NET geliştiriciler güvenilir koleksiyonlar aracılığıyla bir durum bilgisi olan sunar. Özellikle, Service Fabric güvenilir sözlük ve güvenilir sıra sınıfları sağlar. Bu sınıfların kullandığınızda, durumunuza (ölçeklenebilirlik) bölümlenmiş çoğaltılan (kullanılabilirlik için) ve (ACID semantiği için) bir bölüm içinde hareket gerçekleşti. Şimdi tipik bir güvenilir sözlük nesnesi kullanım bakın ve hangi kendi gerçekte yapılması bakın.

```csharp

///retry:

try {
   // Create a new Transaction object for this partition
   using (ITransaction tx = base.StateManager.CreateTransaction()) {
      // AddAsync takes key's write lock; if >4 secs, TimeoutException
      // Key & value put in temp dictionary (read your own writes),
      // serialized, redo/undo record is logged & sent to
      // secondary replicas
      await m_dic.AddAsync(tx, key, value, cancellationToken);

      // CommitAsync sends Commit record toolog & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record toolog & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

Güvenilir sözlük nesnelerine (dışında ClearAsync) geri alınamaz değil, tüm işlemler ITransaction nesneyi gerektirir. Bu nesne ile toomake tooany güvenilir sözlük ve/veya tek bir bölüm içinde güvenilir sıra nesneleri denediğiniz tüm değişiklikleri ilişkilendirilir. Bir ITransaction elde hello bölüm çağırarak nesne kullanıcının StateManager'ın CreateTransaction yöntemi.

Yukarıdaki Hello kod içinde tooa güvenilir sözlüğün AddAsync yöntemi hello ITransaction nesnesinden geçirilir. Dahili olarak, bir anahtar kabul sözlük yöntemleri hello anahtar ile ilişkili bir Okuyucu/Yazıcı kilit etkinleştirilir. Merhaba yöntemi hello anahtarın değerini değiştirirse, hello yöntemi yazma kilidi hello anahtarını alır. ve ardından hello yöntemi yalnızca hello anahtarın değerini yazıyorsa, okuma kilidi hello anahtarı alınır. Hello anahtarın değerini toohello yeni AddAsync değiştirir beri geçen değeri, hello anahtarın yazma kilidi alınır. 2 (veya daha fazla) iş parçacıklarının hello tooadd değerlerle çalışırsanız bu nedenle, aynı hello aynı anahtar zaman, bir iş parçacığı hello yazma kilidi elde ve hello başka bir iş parçacığı engeller. Varsayılan olarak, yöntemleri too4 saniye tooacquire hello Kilidi'ni için engelle; 4 saniye sonra hello yöntemleri bir TimeoutException atar. Dilerseniz yöntemi aşırı yüklemelerine izin verme, toopass açık zaman aşımı değeri mevcut.

Genellikle, bu yakalama ve hello tüm işlemi (yukarıdaki hello kodu gösterildiği gibi) denemeden tarafından kod tooreact tooa TimeoutException yazma. Basit kodumu yalnızca 100 milisaniyede her zaman geçirme Task.Delay aradığım. Ancak, gerçekte üstel geri alma gecikme çeşit kullanmayı devre dışı daha iyi olabilir.

Hello kilit edinilen sonra AddAsync hello anahtar ekler ve tooan iç geçici sözlük hello ITransaction nesneyle ilişkili değer nesnesine başvuruyor. Bu tooprovide yapılır okuma-bilgisayarınızı-kendi-yazma işlemleri semantiği ile. Diğer bir deyişle, AddAsync, bir sonraki çağrı tooTryGetValueAsync çağırdıktan sonra (aynı ITransaction nesne hello kullanarak), henüz hello işlem taahhüt değil olsa bile hello değeri döndürür. Ardından, anahtarınızı AddAsync serileştirir ve değer toobyte diziler nesneleri ve bu bayt dizileri tooa günlük dosyası hello yerel düğümdeki ekler. Son olarak, AddAsync sahip hello şekilde aynı hello bayt dizileri tooall hello ikincil çoğaltmaları anahtar/değer bilgi gönderir. Merhaba anahtar/değer bilgi tooa günlük dosyası yazılmış olsa bile, hello bilgi ile ilişkili hello işlem kaydedilene kadar hello sözlük parçası dikkate alınmaz.

Yukarıdaki Hello kod içinde hello çağrısı tooCommitAsync tüm hello hareketin işlemlerini kaydeder. Özellikle, tamamlama bilgileri toohello günlük dosyası hello yerel düğümdeki ekler ve ayrıca hello yürütme kaydı tooall hello ikincil çoğaltmaları gönderir. Çekirdek (çoğunluğu) hello çoğaltmalarının vermiş sonra tüm veri değişiklikleri kalıcı ve kilitleri hello ITransaction nesnesi yönetilebilir anahtarlarla ilişkili diğer iş parçacıkları/işlemleri işleyebileceğiniz şekilde yayımlandığında değerlendirilir aynı anahtarları hello ve bunların değerleri.

CommitAsync (oluşturulan genellikle tooan özel durum) çağrılmazsa hello ITransaction nesne atıldı. Ne zaman kaydedilmemiş ITransaction nesneyi atma, Service Fabric iptal bilgilerini toohello yerel düğümün günlük dosyası ekler ve hiçbir şey toobe gerekiyor hello tooany ikincil çoğaltmaları gönderdi. Ve ardından hello işlem yönetilebilir anahtarlarla ilişkili kilitleri serbest bırakılır.

## <a name="common-pitfalls-and-how-tooavoid-them"></a>Ortak Tuzaklar ve nasıl tooavoid bunları
Merhaba güvenilir koleksiyonları dahili olarak nasıl çalıştığını anlamak, bazı ortak misuses bunların bir göz atalım. Merhaba kodu aşağıya bakın:

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes hello name/user, logs hello bytes,
   // & sends hello bytes toohello secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // hello line below updates hello property’s value in memory only; the
   // new value is NOT serialized, logged, & sent toosecondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

Normal bir .NET sözlüğü ile çalışırken, bir anahtar/değer toohello sözlük ekleyin ve ardından hello (LastLogin gibi) bir özelliğin değerini değiştirin. Ancak, bu kod ile güvenilir bir sözlük düzgün çalışmaz. Unutmayın hello önceki tartışma, tooAddAsync serileştiren hello anahtar/değer hello çağrısı toobyte diziler nesneleri ve daha sonra kaydeder hello tooa yerel dosya diziler ve ayrıca bunları toohello ikincil çoğaltmaları gönderir. Bir özellik daha sonra değiştirirseniz, bu yalnızca bellekte hello özelliğin değerini değiştirir; Merhaba yerel dosya veya toohello çoğaltmaları gönderilen hello verileri etkilemez. Merhaba işlem çökerse bellekte nedir hemen atılır. Yeni bir işlem başlatıldığında veya başka bir çoğaltma birincil hale gelirse eski özellik değeri hello ne kullanılabilir.

Yeterli ne kadar kolay yukarıda gösterilen hata toomake hello türü olduğunu stres olamaz. Ve hello işlem arıza hello hata hakkında IF/olduğunda yalnızca öğreneceksiniz. Merhaba doğru bir şekilde toowrite hello kodu yalnızca tooreverse hello iki satır verilmiştir:


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

Aşağıda, bir ortak hata gösteren başka bir örnek verilmiştir:

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (user.HasValue) {
      // hello line below updates hello property’s value in memory only; the
      // new value is NOT serialized, logged, & sent toosecondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

Yeniden normal .NET sözlükler, yukarıdaki hello kod düzgün çalışır ve ortak bir desen: hello Geliştirici anahtar toolook değeri kullanır. Başlangıç değeri varsa, hello geliştirici bir özelliğin değerini değiştirir. Ancak, bu kodu güvenilir koleksiyonlarla aynı sorun zaten ele alınan hello sergiler: **tooa güvenilir koleksiyonu verdiğiniz sonra bir nesne değiştirmemelisiniz.**

Merhaba yolu tooupdate güvenilir bir koleksiyonda bir değer tooget bir başvuru toohello mevcut değer ve hello nesne tooby değişmez bu başvuru başvurulan göz önünde bulundurun doğru. Ardından, hello özgün nesne tam bir kopyası olan yeni bir nesne oluşturun. Şimdi, bu yeni nesnenin hello durumu değiştirebilir ve böylece seri hale hello yeni nesne hello koleksiyona toobyte diziler, eklenmiş toohello yerel dosya ve toohello çoğaltmaları gönderilen yazma. Merhaba gerçekleştirmeden, change(s) hello bellek içi nesneleri, hello yerel dosya ve tüm hello çoğaltmalar Merhaba sahip sonra aynı durumu tam. Tüm iyi!

Aşağıdaki Hello kodu hello doğru bir şekilde tooupdate güvenilir bir koleksiyonda bulunan bir değer gösterir:

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use hello user’s name toolook up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // hello user exists in hello dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with hello same state as hello current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In hello new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update hello key’s value toohello updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a>Sabit veri türleri tooprevent Programcı hatası tanımla
İdeal olarak, yanlışlıkla tooconsider değişmez beklenen bir nesnenin durumu değiştirdiği kod üretmek zaman hello derleyici tooreport hataları isteriz. Ancak hello C# Derleyici bu hello özelliği toodo yok. Bu nedenle, tooavoid olası Programcı hatalar, yüksek oranda güvenilir koleksiyonları toobe değişmez türleriyle kullandığınız hello türlerini tanımlayın öneririz. Özellikle, bu toocore değer türleri (örneğin, numaraları [Int32, UInt64, vb.], DateTime, Guid, TimeSpan ve hello gibi) takılıyor anlamına gelir. Ve tabi ki, ayrıca dize kullanabilirsiniz. Seri hale getirme olarak en iyi tooavoid koleksiyon özellikleri olan ve bunları seri durumdan sık performansa zarar verebilir. Ancak, toouse koleksiyon özellikleri istiyorsanız, yüksek oranda hello kullanılmasını öneririz. NET'in değişmez koleksiyonlar kitaplığı ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)). Bu kitaplık http://nuget.org karşıdan yüklenebilir. Ayrıca, sınıflarınızı mühürleme ve mümkün olduğunda alanları salt okunur yapma öneririz.

Merhaba aşağıdaki kullanıcı bilgisi türünü nasıl toodefine sabit bir yazın yararlanarak daha önce bahsedilen öneriler gösterir.

```csharp

[DataContract]
// If you don’t seal, you must ensure that any derived classes are also immutable
public sealed class UserInfo {
   private static readonly IEnumerable<ItemId> NoBids = ImmutableList<ItemId>.Empty;

   public UserInfo(String email, IEnumerable<ItemId> itemsBidding = null) {
      Email = email;
      ItemsBidding = (itemsBidding == null) ? NoBids : itemsBidding.ToImmutableList();
   }

   [OnDeserialized]
   private void OnDeserialized(StreamingContext context) {
      // Convert hello deserialized collection tooan immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has tooset it. So instead, hello getter is public and hello setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId toohello ItemsBidding
   // collection by creating a new immutable UserInfo object with hello added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

Merhaba ItemId türü de aşağıda gösterildiği gibi sabit bir tür olan:

```csharp

[DataContract]
public struct ItemId {

   [DataMember] public readonly String Seller;
   [DataMember] public readonly String ItemName;
   public ItemId(String seller, String itemName) {
      Seller = seller;
      ItemName = itemName;
   }
}
```

## <a name="schema-versioning-upgrades"></a>Şema sürüm oluşturma (yükseltme)
Dahili olarak, güvenilir koleksiyonları kullanarak nesnelerinizin seri hale. NET'in DataContractSerializer. Serileştirilmiş hello nesneleri kalıcı toohello birincil kopyanın yerel disk ve ayrıca iletilen toohello ikincil çoğaltmaları. Hizmetinizi geliştikçe toochange hello tür hizmetiniz için gerekli verileri (şema) isteyeceksiniz olasıdır. Sürüm oluşturma dikkatli verilerinizin yaklaşımını gerekir. Öncelikle, her zaman mümkün toodeserialize eski verileri olması gerekir. Özellikle, bu seri durumdan çıkarma kodunuzu sonsuz geriye dönük olarak uyumlu olmalıdır anlamına gelir: sürüm 333 service kodunuzun mümkün toooperate güvenilir bir koleksiyonda 5 yıl önce hizmet kodunuzun 1 sürümü tarafından yerleştirilen veriler üzerinde olmalıdır.

Ayrıca, hizmet yükseltilen bir yükseltme etki alanı aynı anda kodudur. Bu nedenle, yükseltme sırasında hizmet kodunuzun eşzamanlı çalışan iki farklı sürümü gerekir. Hizmet kodunuzun eski sürümlerini mümkün toohandle hello yeni şema olmayabilir gibi hello yeni şema kullanın hello yeni sürümünü service kodunuzun olmamasına özen gösterin gerekir. Mümkün olduğunda, hizmet toobe ileri doğru uyumlu her sürümü 1 sürümüne göre tasarlamanız gerekir. Özellikle, bu hizmet kodunuzun V1 mümkün olması anlamına gelir toosimply, açıkça işlemiyor hiçbir şema öğeleri yoksay. Ancak, bir sözlük anahtar veya değer güncelleştirilirken açıkça bilmeniz değil ve yalnızca yazma herhangi bir veri yedekleme çıkışı mümkün toosave olması gerekir.

> [!WARNING]
> Anahtar hello şema değiştirebilirsiniz, ancak, anahtarın karma kodu ve eşittir algoritmaları kararlı olduğundan emin olmalısınız. Bu algoritmalar birini nasıl çalıştığını değiştirirseniz, mümkün toolook hello anahtarı hello güvenilir sözlük içinde herhangi bir zamanda yeniden olmaz.
>
>

Alternatif olarak, ne olduğunu genellikle başvurulan tooas 2 aşamalı yükseltme gerçekleştirebilirsiniz. Aşama 2 yükseltme işlemine V1 tooV2 hizmetinizi yükseltme: V2 toodeal hello yeni şema değişikliği ancak bu kodu nasıl yürütmez bilir hello kodunu içerir. Merhaba V2 kod V1 veri okuduğunda üzerinde çalışır ve V1 verileri yazar. Tüm yükseltme etki alanları arasında Hello yükseltme tamamlandıktan sonra daha sonra şekilde toohello çalışan V2 örneklerini bu hello yükseltme tamamlandıktan sinyal. (Tek yönlü toosignal bu yapılandırma yükseltme çıkışı tooroll; Bu aşama 2 yükseltme yapar budur.) Şimdi, hello V2 örnekleri V1 veri okuma, tooV2 verileri dönüştürmek, üzerinde çalışır ve V2 verileri olarak yazamadı. Diğer örnekleri V2 veri okuma, tooconvert gereksinim değildir, bunlar yalnızca üzerinde çalışır ve V2 verileri yazma.

## <a name="next-steps"></a>Sonraki Adımlar
İleri uyumlu veri sözleşmeleri oluşturma hakkında daha fazla toolearn bkz [İleri uyumlu veri sözleşmeleri](https://msdn.microsoft.com/library/ms731083.aspx).

sürüm oluşturma veri sözleşmelerinde toolearn en iyi yöntemler bkz [veri sözleşmesi sürümü oluşturma](https://msdn.microsoft.com/library/ms731138.aspx).

tooimplement sürüm dayanıklı veri sözleşmeleri toolearn bkz [sürüm toleranslı seri hale getirme geri çağrıları](https://msdn.microsoft.com/library/ms733734.aspx).

tooprovide birden çok sürümleri arasında çalışabilirler bir veri yapısı nasıl görürüm toolearn [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).
