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
# <a name="working-with-reliable-collections"></a><span data-ttu-id="f790e-103">Güvenilir koleksiyonları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="f790e-103">Working with Reliable Collections</span></span>
<span data-ttu-id="f790e-104">Service Fabric programlama modeli kullanılabilir too.NET geliştiriciler güvenilir koleksiyonlar aracılığıyla bir durum bilgisi olan sunar.</span><span class="sxs-lookup"><span data-stu-id="f790e-104">Service Fabric offers a stateful programming model available too.NET developers via Reliable Collections.</span></span> <span data-ttu-id="f790e-105">Özellikle, Service Fabric güvenilir sözlük ve güvenilir sıra sınıfları sağlar.</span><span class="sxs-lookup"><span data-stu-id="f790e-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="f790e-106">Bu sınıfların kullandığınızda, durumunuza (ölçeklenebilirlik) bölümlenmiş çoğaltılan (kullanılabilirlik için) ve (ACID semantiği için) bir bölüm içinde hareket gerçekleşti.</span><span class="sxs-lookup"><span data-stu-id="f790e-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="f790e-107">Şimdi tipik bir güvenilir sözlük nesnesi kullanım bakın ve hangi kendi gerçekte yapılması bakın.</span><span class="sxs-lookup"><span data-stu-id="f790e-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

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

<span data-ttu-id="f790e-108">Güvenilir sözlük nesnelerine (dışında ClearAsync) geri alınamaz değil, tüm işlemler ITransaction nesneyi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f790e-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="f790e-109">Bu nesne ile toomake tooany güvenilir sözlük ve/veya tek bir bölüm içinde güvenilir sıra nesneleri denediğiniz tüm değişiklikleri ilişkilendirilir.</span><span class="sxs-lookup"><span data-stu-id="f790e-109">This object has associated with it any and all changes you’re attempting toomake tooany reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="f790e-110">Bir ITransaction elde hello bölüm çağırarak nesne kullanıcının StateManager'ın CreateTransaction yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f790e-110">You acquire an ITransaction object by calling hello partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="f790e-111">Yukarıdaki Hello kod içinde tooa güvenilir sözlüğün AddAsync yöntemi hello ITransaction nesnesinden geçirilir.</span><span class="sxs-lookup"><span data-stu-id="f790e-111">In hello code above, hello ITransaction object is passed tooa reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="f790e-112">Dahili olarak, bir anahtar kabul sözlük yöntemleri hello anahtar ile ilişkili bir Okuyucu/Yazıcı kilit etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f790e-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with hello key.</span></span> <span data-ttu-id="f790e-113">Merhaba yöntemi hello anahtarın değerini değiştirirse, hello yöntemi yazma kilidi hello anahtarını alır. ve ardından hello yöntemi yalnızca hello anahtarın değerini yazıyorsa, okuma kilidi hello anahtarı alınır.</span><span class="sxs-lookup"><span data-stu-id="f790e-113">If hello method modifies hello key’s value, hello method takes a write lock on hello key and if hello method only reads from hello key’s value, then a read lock is taken on hello key.</span></span> <span data-ttu-id="f790e-114">Hello anahtarın değerini toohello yeni AddAsync değiştirir beri geçen değeri, hello anahtarın yazma kilidi alınır.</span><span class="sxs-lookup"><span data-stu-id="f790e-114">Since AddAsync modifies hello key’s value toohello new, passed-in value, hello key’s write lock is taken.</span></span> <span data-ttu-id="f790e-115">2 (veya daha fazla) iş parçacıklarının hello tooadd değerlerle çalışırsanız bu nedenle, aynı hello aynı anahtar zaman, bir iş parçacığı hello yazma kilidi elde ve hello başka bir iş parçacığı engeller.</span><span class="sxs-lookup"><span data-stu-id="f790e-115">So, if 2 (or more) threads attempt tooadd values with hello same key at hello same time, one thread will acquire hello write lock and hello other threads will block.</span></span> <span data-ttu-id="f790e-116">Varsayılan olarak, yöntemleri too4 saniye tooacquire hello Kilidi'ni için engelle; 4 saniye sonra hello yöntemleri bir TimeoutException atar.</span><span class="sxs-lookup"><span data-stu-id="f790e-116">By default, methods block for up too4 seconds tooacquire hello lock; after 4 seconds, hello methods throw a TimeoutException.</span></span> <span data-ttu-id="f790e-117">Dilerseniz yöntemi aşırı yüklemelerine izin verme, toopass açık zaman aşımı değeri mevcut.</span><span class="sxs-lookup"><span data-stu-id="f790e-117">Method overloads exist allowing you toopass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="f790e-118">Genellikle, bu yakalama ve hello tüm işlemi (yukarıdaki hello kodu gösterildiği gibi) denemeden tarafından kod tooreact tooa TimeoutException yazma.</span><span class="sxs-lookup"><span data-stu-id="f790e-118">Usually, you write your code tooreact tooa TimeoutException by catching it and retrying hello entire operation (as shown in hello code above).</span></span> <span data-ttu-id="f790e-119">Basit kodumu yalnızca 100 milisaniyede her zaman geçirme Task.Delay aradığım.</span><span class="sxs-lookup"><span data-stu-id="f790e-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="f790e-120">Ancak, gerçekte üstel geri alma gecikme çeşit kullanmayı devre dışı daha iyi olabilir.</span><span class="sxs-lookup"><span data-stu-id="f790e-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="f790e-121">Hello kilit edinilen sonra AddAsync hello anahtar ekler ve tooan iç geçici sözlük hello ITransaction nesneyle ilişkili değer nesnesine başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="f790e-121">Once hello lock is acquired, AddAsync adds hello key and value object references tooan internal temporary dictionary associated with hello ITransaction object.</span></span> <span data-ttu-id="f790e-122">Bu tooprovide yapılır okuma-bilgisayarınızı-kendi-yazma işlemleri semantiği ile.</span><span class="sxs-lookup"><span data-stu-id="f790e-122">This is done tooprovide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="f790e-123">Diğer bir deyişle, AddAsync, bir sonraki çağrı tooTryGetValueAsync çağırdıktan sonra (aynı ITransaction nesne hello kullanarak), henüz hello işlem taahhüt değil olsa bile hello değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="f790e-123">That is, after you call AddAsync, a later call tooTryGetValueAsync (using hello same ITransaction object) will return hello value even if you have not yet committed hello transaction.</span></span> <span data-ttu-id="f790e-124">Ardından, anahtarınızı AddAsync serileştirir ve değer toobyte diziler nesneleri ve bu bayt dizileri tooa günlük dosyası hello yerel düğümdeki ekler.</span><span class="sxs-lookup"><span data-stu-id="f790e-124">Next, AddAsync serializes your key and value objects toobyte arrays and appends these byte arrays tooa log file on hello local node.</span></span> <span data-ttu-id="f790e-125">Son olarak, AddAsync sahip hello şekilde aynı hello bayt dizileri tooall hello ikincil çoğaltmaları anahtar/değer bilgi gönderir.</span><span class="sxs-lookup"><span data-stu-id="f790e-125">Finally, AddAsync sends hello byte arrays tooall hello secondary replicas so they have hello same key/value information.</span></span> <span data-ttu-id="f790e-126">Merhaba anahtar/değer bilgi tooa günlük dosyası yazılmış olsa bile, hello bilgi ile ilişkili hello işlem kaydedilene kadar hello sözlük parçası dikkate alınmaz.</span><span class="sxs-lookup"><span data-stu-id="f790e-126">Even though hello key/value information has been written tooa log file, hello information is not considered part of hello dictionary until hello transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="f790e-127">Yukarıdaki Hello kod içinde hello çağrısı tooCommitAsync tüm hello hareketin işlemlerini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="f790e-127">In hello code above, hello call tooCommitAsync commits all of hello transaction’s operations.</span></span> <span data-ttu-id="f790e-128">Özellikle, tamamlama bilgileri toohello günlük dosyası hello yerel düğümdeki ekler ve ayrıca hello yürütme kaydı tooall hello ikincil çoğaltmaları gönderir.</span><span class="sxs-lookup"><span data-stu-id="f790e-128">Specifically, it appends commit information toohello log file on hello local node and also sends hello commit record tooall hello secondary replicas.</span></span> <span data-ttu-id="f790e-129">Çekirdek (çoğunluğu) hello çoğaltmalarının vermiş sonra tüm veri değişiklikleri kalıcı ve kilitleri hello ITransaction nesnesi yönetilebilir anahtarlarla ilişkili diğer iş parçacıkları/işlemleri işleyebileceğiniz şekilde yayımlandığında değerlendirilir aynı anahtarları hello ve bunların değerleri.</span><span class="sxs-lookup"><span data-stu-id="f790e-129">Once a quorum (majority) of hello replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via hello ITransaction object are released so other threads/transactions can manipulate hello same keys and their values.</span></span>

<span data-ttu-id="f790e-130">CommitAsync (oluşturulan genellikle tooan özel durum) çağrılmazsa hello ITransaction nesne atıldı.</span><span class="sxs-lookup"><span data-stu-id="f790e-130">If CommitAsync is not called (usually due tooan exception being thrown), then hello ITransaction object gets disposed.</span></span> <span data-ttu-id="f790e-131">Ne zaman kaydedilmemiş ITransaction nesneyi atma, Service Fabric iptal bilgilerini toohello yerel düğümün günlük dosyası ekler ve hiçbir şey toobe gerekiyor hello tooany ikincil çoğaltmaları gönderdi.</span><span class="sxs-lookup"><span data-stu-id="f790e-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information toohello local node’s log file and nothing needs toobe sent tooany of hello secondary replicas.</span></span> <span data-ttu-id="f790e-132">Ve ardından hello işlem yönetilebilir anahtarlarla ilişkili kilitleri serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="f790e-132">And then, any locks associated with keys that were manipulated via hello transaction are released.</span></span>

## <a name="common-pitfalls-and-how-tooavoid-them"></a><span data-ttu-id="f790e-133">Ortak Tuzaklar ve nasıl tooavoid bunları</span><span class="sxs-lookup"><span data-stu-id="f790e-133">Common pitfalls and how tooavoid them</span></span>
<span data-ttu-id="f790e-134">Merhaba güvenilir koleksiyonları dahili olarak nasıl çalıştığını anlamak, bazı ortak misuses bunların bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="f790e-134">Now that you understand how hello reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="f790e-135">Merhaba kodu aşağıya bakın:</span><span class="sxs-lookup"><span data-stu-id="f790e-135">See hello code below:</span></span>

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

<span data-ttu-id="f790e-136">Normal bir .NET sözlüğü ile çalışırken, bir anahtar/değer toohello sözlük ekleyin ve ardından hello (LastLogin gibi) bir özelliğin değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f790e-136">When working with a regular .NET dictionary, you can add a key/value toohello dictionary and then change hello value of a property (such as LastLogin).</span></span> <span data-ttu-id="f790e-137">Ancak, bu kod ile güvenilir bir sözlük düzgün çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="f790e-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="f790e-138">Unutmayın hello önceki tartışma, tooAddAsync serileştiren hello anahtar/değer hello çağrısı toobyte diziler nesneleri ve daha sonra kaydeder hello tooa yerel dosya diziler ve ayrıca bunları toohello ikincil çoğaltmaları gönderir.</span><span class="sxs-lookup"><span data-stu-id="f790e-138">Remember from hello earlier discussion, hello call tooAddAsync serializes hello key/value objects toobyte arrays and then saves hello arrays tooa local file and also sends them toohello secondary replicas.</span></span> <span data-ttu-id="f790e-139">Bir özellik daha sonra değiştirirseniz, bu yalnızca bellekte hello özelliğin değerini değiştirir; Merhaba yerel dosya veya toohello çoğaltmaları gönderilen hello verileri etkilemez.</span><span class="sxs-lookup"><span data-stu-id="f790e-139">If you later change a property, this changes hello property’s value in memory only; it does not impact hello local file or hello data sent toohello replicas.</span></span> <span data-ttu-id="f790e-140">Merhaba işlem çökerse bellekte nedir hemen atılır.</span><span class="sxs-lookup"><span data-stu-id="f790e-140">If hello process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="f790e-141">Yeni bir işlem başlatıldığında veya başka bir çoğaltma birincil hale gelirse eski özellik değeri hello ne kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f790e-141">When a new process starts or if another replica becomes primary, then hello old property value is what is available.</span></span>

<span data-ttu-id="f790e-142">Yeterli ne kadar kolay yukarıda gösterilen hata toomake hello türü olduğunu stres olamaz.</span><span class="sxs-lookup"><span data-stu-id="f790e-142">I cannot stress enough how easy it is toomake hello kind of mistake shown above.</span></span> <span data-ttu-id="f790e-143">Ve hello işlem arıza hello hata hakkında IF/olduğunda yalnızca öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f790e-143">And, you will only learn about hello mistake if/when hello process goes down.</span></span> <span data-ttu-id="f790e-144">Merhaba doğru bir şekilde toowrite hello kodu yalnızca tooreverse hello iki satır verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f790e-144">hello correct way toowrite hello code is simply tooreverse hello two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="f790e-145">Aşağıda, bir ortak hata gösteren başka bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="f790e-145">Here is another example showing a common mistake:</span></span>

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

<span data-ttu-id="f790e-146">Yeniden normal .NET sözlükler, yukarıdaki hello kod düzgün çalışır ve ortak bir desen: hello Geliştirici anahtar toolook değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="f790e-146">Again, with regular .NET dictionaries, hello code above works fine and is a common pattern: hello developer uses a key toolook up a value.</span></span> <span data-ttu-id="f790e-147">Başlangıç değeri varsa, hello geliştirici bir özelliğin değerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="f790e-147">If hello value exists, hello developer changes a property’s value.</span></span> <span data-ttu-id="f790e-148">Ancak, bu kodu güvenilir koleksiyonlarla aynı sorun zaten ele alınan hello sergiler: **tooa güvenilir koleksiyonu verdiğiniz sonra bir nesne değiştirmemelisiniz.**</span><span class="sxs-lookup"><span data-stu-id="f790e-148">However, with reliable collections, this code exhibits hello same problem as already discussed: **you MUST not modify an object once you have given it tooa reliable collection.**</span></span>

<span data-ttu-id="f790e-149">Merhaba yolu tooupdate güvenilir bir koleksiyonda bir değer tooget bir başvuru toohello mevcut değer ve hello nesne tooby değişmez bu başvuru başvurulan göz önünde bulundurun doğru.</span><span class="sxs-lookup"><span data-stu-id="f790e-149">hello correct way tooupdate a value in a reliable collection, is tooget a reference toohello existing value and consider hello object referred tooby this reference immutable.</span></span> <span data-ttu-id="f790e-150">Ardından, hello özgün nesne tam bir kopyası olan yeni bir nesne oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f790e-150">Then, create a new object which is an exact copy of hello original object.</span></span> <span data-ttu-id="f790e-151">Şimdi, bu yeni nesnenin hello durumu değiştirebilir ve böylece seri hale hello yeni nesne hello koleksiyona toobyte diziler, eklenmiş toohello yerel dosya ve toohello çoğaltmaları gönderilen yazma.</span><span class="sxs-lookup"><span data-stu-id="f790e-151">Now, you can modify hello state of this new object and write hello new object into hello collection so that it gets serialized toobyte arrays, appended toohello local file and sent toohello replicas.</span></span> <span data-ttu-id="f790e-152">Merhaba gerçekleştirmeden, change(s) hello bellek içi nesneleri, hello yerel dosya ve tüm hello çoğaltmalar Merhaba sahip sonra aynı durumu tam.</span><span class="sxs-lookup"><span data-stu-id="f790e-152">After committing hello change(s), hello in-memory objects, hello local file, and all hello replicas have hello same exact state.</span></span> <span data-ttu-id="f790e-153">Tüm iyi!</span><span class="sxs-lookup"><span data-stu-id="f790e-153">All is good!</span></span>

<span data-ttu-id="f790e-154">Aşağıdaki Hello kodu hello doğru bir şekilde tooupdate güvenilir bir koleksiyonda bulunan bir değer gösterir:</span><span class="sxs-lookup"><span data-stu-id="f790e-154">hello code below shows hello correct way tooupdate a value in a reliable collection:</span></span>

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

## <a name="define-immutable-data-types-tooprevent-programmer-error"></a><span data-ttu-id="f790e-155">Sabit veri türleri tooprevent Programcı hatası tanımla</span><span class="sxs-lookup"><span data-stu-id="f790e-155">Define immutable data types tooprevent programmer error</span></span>
<span data-ttu-id="f790e-156">İdeal olarak, yanlışlıkla tooconsider değişmez beklenen bir nesnenin durumu değiştirdiği kod üretmek zaman hello derleyici tooreport hataları isteriz.</span><span class="sxs-lookup"><span data-stu-id="f790e-156">Ideally, we’d like hello compiler tooreport errors when you accidentally produce code that mutates state of an object that you are supposed tooconsider immutable.</span></span> <span data-ttu-id="f790e-157">Ancak hello C# Derleyici bu hello özelliği toodo yok.</span><span class="sxs-lookup"><span data-stu-id="f790e-157">But, hello C# compiler does not have hello ability toodo this.</span></span> <span data-ttu-id="f790e-158">Bu nedenle, tooavoid olası Programcı hatalar, yüksek oranda güvenilir koleksiyonları toobe değişmez türleriyle kullandığınız hello türlerini tanımlayın öneririz.</span><span class="sxs-lookup"><span data-stu-id="f790e-158">So, tooavoid potential programmer bugs, we highly recommend that you define hello types you use with reliable collections toobe immutable types.</span></span> <span data-ttu-id="f790e-159">Özellikle, bu toocore değer türleri (örneğin, numaraları [Int32, UInt64, vb.], DateTime, Guid, TimeSpan ve hello gibi) takılıyor anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="f790e-159">Specifically, this means that you stick toocore value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and hello like).</span></span> <span data-ttu-id="f790e-160">Ve tabi ki, ayrıca dize kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f790e-160">And, of course, you can also use String.</span></span> <span data-ttu-id="f790e-161">Seri hale getirme olarak en iyi tooavoid koleksiyon özellikleri olan ve bunları seri durumdan sık performansa zarar verebilir.</span><span class="sxs-lookup"><span data-stu-id="f790e-161">It is best tooavoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="f790e-162">Ancak, toouse koleksiyon özellikleri istiyorsanız, yüksek oranda hello kullanılmasını öneririz. NET'in değişmez koleksiyonlar kitaplığı ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="f790e-162">However, if you want toouse collection properties, we highly recommend hello use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="f790e-163">Bu kitaplık http://nuget.org karşıdan yüklenebilir. Ayrıca, sınıflarınızı mühürleme ve mümkün olduğunda alanları salt okunur yapma öneririz.</span><span class="sxs-lookup"><span data-stu-id="f790e-163">This library is available for download from http://nuget.org. We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="f790e-164">Merhaba aşağıdaki kullanıcı bilgisi türünü nasıl toodefine sabit bir yazın yararlanarak daha önce bahsedilen öneriler gösterir.</span><span class="sxs-lookup"><span data-stu-id="f790e-164">hello UserInfo type below demonstrates how toodefine an immutable type taking advantage of aforementioned recommendations.</span></span>

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

<span data-ttu-id="f790e-165">Merhaba ItemId türü de aşağıda gösterildiği gibi sabit bir tür olan:</span><span class="sxs-lookup"><span data-stu-id="f790e-165">hello ItemId type is also an immutable type as shown here:</span></span>

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

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="f790e-166">Şema sürüm oluşturma (yükseltme)</span><span class="sxs-lookup"><span data-stu-id="f790e-166">Schema versioning (upgrades)</span></span>
<span data-ttu-id="f790e-167">Dahili olarak, güvenilir koleksiyonları kullanarak nesnelerinizin seri hale. NET'in DataContractSerializer.</span><span class="sxs-lookup"><span data-stu-id="f790e-167">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="f790e-168">Serileştirilmiş hello nesneleri kalıcı toohello birincil kopyanın yerel disk ve ayrıca iletilen toohello ikincil çoğaltmaları.</span><span class="sxs-lookup"><span data-stu-id="f790e-168">hello serialized objects are persisted toohello primary replica’s local disk and are also transmitted toohello secondary replicas.</span></span> <span data-ttu-id="f790e-169">Hizmetinizi geliştikçe toochange hello tür hizmetiniz için gerekli verileri (şema) isteyeceksiniz olasıdır.</span><span class="sxs-lookup"><span data-stu-id="f790e-169">As your service matures, it’s likely you’ll want toochange hello kind of data (schema) your service requires.</span></span> <span data-ttu-id="f790e-170">Sürüm oluşturma dikkatli verilerinizin yaklaşımını gerekir.</span><span class="sxs-lookup"><span data-stu-id="f790e-170">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="f790e-171">Öncelikle, her zaman mümkün toodeserialize eski verileri olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f790e-171">First and foremost, you must always be able toodeserialize old data.</span></span> <span data-ttu-id="f790e-172">Özellikle, bu seri durumdan çıkarma kodunuzu sonsuz geriye dönük olarak uyumlu olmalıdır anlamına gelir: sürüm 333 service kodunuzun mümkün toooperate güvenilir bir koleksiyonda 5 yıl önce hizmet kodunuzun 1 sürümü tarafından yerleştirilen veriler üzerinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f790e-172">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able toooperate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="f790e-173">Ayrıca, hizmet yükseltilen bir yükseltme etki alanı aynı anda kodudur.</span><span class="sxs-lookup"><span data-stu-id="f790e-173">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="f790e-174">Bu nedenle, yükseltme sırasında hizmet kodunuzun eşzamanlı çalışan iki farklı sürümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="f790e-174">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="f790e-175">Hizmet kodunuzun eski sürümlerini mümkün toohandle hello yeni şema olmayabilir gibi hello yeni şema kullanın hello yeni sürümünü service kodunuzun olmamasına özen gösterin gerekir.</span><span class="sxs-lookup"><span data-stu-id="f790e-175">You must avoid having hello new version of your service code use hello new schema as old versions of your service code might not be able toohandle hello new schema.</span></span> <span data-ttu-id="f790e-176">Mümkün olduğunda, hizmet toobe ileri doğru uyumlu her sürümü 1 sürümüne göre tasarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f790e-176">When possible, you should design each version of your service toobe forward compatible by 1 version.</span></span> <span data-ttu-id="f790e-177">Özellikle, bu hizmet kodunuzun V1 mümkün olması anlamına gelir toosimply, açıkça işlemiyor hiçbir şema öğeleri yoksay.</span><span class="sxs-lookup"><span data-stu-id="f790e-177">Specifically, this means that V1 of your service code should be able toosimply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="f790e-178">Ancak, bir sözlük anahtar veya değer güncelleştirilirken açıkça bilmeniz değil ve yalnızca yazma herhangi bir veri yedekleme çıkışı mümkün toosave olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f790e-178">However, it must be able toosave any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="f790e-179">Anahtar hello şema değiştirebilirsiniz, ancak, anahtarın karma kodu ve eşittir algoritmaları kararlı olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="f790e-179">While you can modify hello schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="f790e-180">Bu algoritmalar birini nasıl çalıştığını değiştirirseniz, mümkün toolook hello anahtarı hello güvenilir sözlük içinde herhangi bir zamanda yeniden olmaz.</span><span class="sxs-lookup"><span data-stu-id="f790e-180">If you change how either of these algorithms operate, you will not be able toolook up hello key within hello reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="f790e-181">Alternatif olarak, ne olduğunu genellikle başvurulan tooas 2 aşamalı yükseltme gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f790e-181">Alternatively, you can perform what is typically referred tooas a 2-phase upgrade.</span></span> <span data-ttu-id="f790e-182">Aşama 2 yükseltme işlemine V1 tooV2 hizmetinizi yükseltme: V2 toodeal hello yeni şema değişikliği ancak bu kodu nasıl yürütmez bilir hello kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="f790e-182">With a 2-phase upgrade, you upgrade your service from V1 tooV2: V2 contains hello code that knows how toodeal with hello new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="f790e-183">Merhaba V2 kod V1 veri okuduğunda üzerinde çalışır ve V1 verileri yazar.</span><span class="sxs-lookup"><span data-stu-id="f790e-183">When hello V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="f790e-184">Tüm yükseltme etki alanları arasında Hello yükseltme tamamlandıktan sonra daha sonra şekilde toohello çalışan V2 örneklerini bu hello yükseltme tamamlandıktan sinyal.</span><span class="sxs-lookup"><span data-stu-id="f790e-184">Then, after hello upgrade is complete across all upgrade domains, you can somehow signal toohello running V2 instances that hello upgrade is complete.</span></span> <span data-ttu-id="f790e-185">(Tek yönlü toosignal bu yapılandırma yükseltme çıkışı tooroll; Bu aşama 2 yükseltme yapar budur.) Şimdi, hello V2 örnekleri V1 veri okuma, tooV2 verileri dönüştürmek, üzerinde çalışır ve V2 verileri olarak yazamadı.</span><span class="sxs-lookup"><span data-stu-id="f790e-185">(One way toosignal this is tooroll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, hello V2 instances can read V1 data, convert it tooV2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="f790e-186">Diğer örnekleri V2 veri okuma, tooconvert gereksinim değildir, bunlar yalnızca üzerinde çalışır ve V2 verileri yazma.</span><span class="sxs-lookup"><span data-stu-id="f790e-186">When other instances read V2 data, they do not need tooconvert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f790e-187">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f790e-187">Next Steps</span></span>
<span data-ttu-id="f790e-188">İleri uyumlu veri sözleşmeleri oluşturma hakkında daha fazla toolearn bkz [İleri uyumlu veri sözleşmeleri](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="f790e-188">toolearn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="f790e-189">sürüm oluşturma veri sözleşmelerinde toolearn en iyi yöntemler bkz [veri sözleşmesi sürümü oluşturma](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="f790e-189">toolearn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="f790e-190">tooimplement sürüm dayanıklı veri sözleşmeleri toolearn bkz [sürüm toleranslı seri hale getirme geri çağrıları](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="f790e-190">toolearn how tooimplement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="f790e-191">tooprovide birden çok sürümleri arasında çalışabilirler bir veri yapısı nasıl görürüm toolearn [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="f790e-191">toolearn how tooprovide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
