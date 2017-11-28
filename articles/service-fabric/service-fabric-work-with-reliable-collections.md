---
title: "Güvenilir koleksiyonları ile çalışma | Microsoft Docs"
description: "Güvenilir koleksiyonları ile çalışmak için en iyi uygulamaları öğrenin."
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
ms.openlocfilehash: f53f13e4fb83b1cd370ec673e86e5311cd93055f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-reliable-collections"></a><span data-ttu-id="7d965-103">Güvenilir koleksiyonları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="7d965-103">Working with Reliable Collections</span></span>
<span data-ttu-id="7d965-104">Service Fabric, güvenilir koleksiyonlar aracılığıyla .NET geliştiricileri için kullanılabilir bir durum bilgisi olan programlama modeli sunar.</span><span class="sxs-lookup"><span data-stu-id="7d965-104">Service Fabric offers a stateful programming model available to .NET developers via Reliable Collections.</span></span> <span data-ttu-id="7d965-105">Özellikle, Service Fabric güvenilir sözlük ve güvenilir sıra sınıfları sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d965-105">Specifically, Service Fabric provides reliable dictionary and reliable queue classes.</span></span> <span data-ttu-id="7d965-106">Bu sınıfların kullandığınızda, durumunuza (ölçeklenebilirlik) bölümlenmiş çoğaltılan (kullanılabilirlik için) ve (ACID semantiği için) bir bölüm içinde hareket gerçekleşti.</span><span class="sxs-lookup"><span data-stu-id="7d965-106">When you use these classes, your state is partitioned (for scalability), replicated (for availability), and transacted within a partition (for ACID semantics).</span></span> <span data-ttu-id="7d965-107">Şimdi tipik bir güvenilir sözlük nesnesi kullanım bakın ve hangi kendi gerçekte yapılması bakın.</span><span class="sxs-lookup"><span data-stu-id="7d965-107">Let’s look at a typical usage of a reliable dictionary object and see what its actually doing.</span></span>

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

      // CommitAsync sends Commit record to log & secondary replicas
      // After quorum responds, all locks released
      await tx.CommitAsync();
   }
   // If CommitAsync not called, Dispose sends Abort
   // record to log & all locks released
}
catch (TimeoutException) {
   await Task.Delay(100, cancellationToken); goto retry;
}
```

<span data-ttu-id="7d965-108">Güvenilir sözlük nesnelerine (dışında ClearAsync) geri alınamaz değil, tüm işlemler ITransaction nesneyi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7d965-108">All operations on reliable dictionary objects (except for ClearAsync which is not undoable), require an ITransaction object.</span></span> <span data-ttu-id="7d965-109">Bu nesne herhangi ilişkili ve güvenilir bir sözlük ve/veya güvenilir yapmaya çalışmadan tüm değişiklikleri tek bir bölüm içindeki nesneleri sıraya.</span><span class="sxs-lookup"><span data-stu-id="7d965-109">This object has associated with it any and all changes you’re attempting to make to any reliable dictionary and/or reliable queue objects within a single partition.</span></span> <span data-ttu-id="7d965-110">Bir ITransaction elde bölüm çağırarak nesne kullanıcının StateManager'ın CreateTransaction yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7d965-110">You acquire an ITransaction object by calling the partition’s StateManager’s CreateTransaction method.</span></span>

<span data-ttu-id="7d965-111">Yukarıdaki kod ITransaction nesne güvenilir sözlüğün AddAsync yöntemine iletilir.</span><span class="sxs-lookup"><span data-stu-id="7d965-111">In the code above, the ITransaction object is passed to a reliable dictionary’s AddAsync method.</span></span> <span data-ttu-id="7d965-112">Dahili olarak, bir anahtar kabul sözlük yöntemleri anahtarıyla ilişkilendirilmiş bir Okuyucu/Yazıcı kilit etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7d965-112">Internally, dictionary methods that accepts a key take a reader/writer lock associated with the key.</span></span> <span data-ttu-id="7d965-113">Yöntemi anahtarın değerini değiştirirse, yöntem bir yazma kilidi anahtarı alır. ve ardından yöntemi yalnızca anahtarın değerini yazıyorsa, okuma kilidi anahtarı alınır.</span><span class="sxs-lookup"><span data-stu-id="7d965-113">If the method modifies the key’s value, the method takes a write lock on the key and if the method only reads from the key’s value, then a read lock is taken on the key.</span></span> <span data-ttu-id="7d965-114">Anahtarın değerini yeni, geçirilen değerle AddAsync değiştirir olduğundan, anahtarın yazma kilidi alınır.</span><span class="sxs-lookup"><span data-stu-id="7d965-114">Since AddAsync modifies the key’s value to the new, passed-in value, the key’s write lock is taken.</span></span> <span data-ttu-id="7d965-115">Bu nedenle, 2 (veya daha fazla) iş parçacığı aynı anda aynı anahtarla değerleri eklemeye çalışırsanız, bir iş parçacığı yazma kilidi ve diğer iş parçacıklarından engeller.</span><span class="sxs-lookup"><span data-stu-id="7d965-115">So, if 2 (or more) threads attempt to add values with the same key at the same time, one thread will acquire the write lock and the other threads will block.</span></span> <span data-ttu-id="7d965-116">Varsayılan olarak, kilit 4 saniye için yöntemleri bloğu; 4 saniye sonra yöntemleri bir TimeoutException atar.</span><span class="sxs-lookup"><span data-stu-id="7d965-116">By default, methods block for up to 4 seconds to acquire the lock; after 4 seconds, the methods throw a TimeoutException.</span></span> <span data-ttu-id="7d965-117">Yöntemi aşırı Dilerseniz bir açık zaman aşımı değeri geçirmek izin yok.</span><span class="sxs-lookup"><span data-stu-id="7d965-117">Method overloads exist allowing you to pass an explicit timeout value if you’d prefer.</span></span>

<span data-ttu-id="7d965-118">Genellikle, bu yakalama ve tüm işlemi (yukarıdaki kodda gösterildiği gibi) denemeden tarafından bir TimeoutException tepki vermek için kodunuzu yazın.</span><span class="sxs-lookup"><span data-stu-id="7d965-118">Usually, you write your code to react to a TimeoutException by catching it and retrying the entire operation (as shown in the code above).</span></span> <span data-ttu-id="7d965-119">Basit kodumu yalnızca 100 milisaniyede her zaman geçirme Task.Delay aradığım.</span><span class="sxs-lookup"><span data-stu-id="7d965-119">In my simple code, I’m just calling Task.Delay passing 100 milliseconds each time.</span></span> <span data-ttu-id="7d965-120">Ancak, gerçekte üstel geri alma gecikme çeşit kullanmayı devre dışı daha iyi olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d965-120">But, in reality, you might be better off using some kind of exponential back-off delay instead.</span></span>

<span data-ttu-id="7d965-121">Kilit edinilen sonra AddAsync ITransaction nesneyle ilişkili bir iç geçici sözlük anahtar ve değer nesne başvuruları ekler.</span><span class="sxs-lookup"><span data-stu-id="7d965-121">Once the lock is acquired, AddAsync adds the key and value object references to an internal temporary dictionary associated with the ITransaction object.</span></span> <span data-ttu-id="7d965-122">Bu, okuma-bilgisayarınızı-kendi-yazma işlemleri semantiği ile sağlamak için gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7d965-122">This is done to provide you with read-your-own-writes semantics.</span></span> <span data-ttu-id="7d965-123">Diğer bir deyişle, AddAsync çağırdıktan sonra dahi, henüz işlem taahhüt değil (aynı ITransaction nesnesi kullanarak) TryGetValueAsync sonraki çağrı değeri döndürür.</span><span class="sxs-lookup"><span data-stu-id="7d965-123">That is, after you call AddAsync, a later call to TryGetValueAsync (using the same ITransaction object) will return the value even if you have not yet committed the transaction.</span></span> <span data-ttu-id="7d965-124">Ardından, anahtarınızı AddAsync serileştirir ve değer bayt dizileri nesneleri ve bu bayt dizileri yerel düğüm üzerindeki bir günlük dosyasına ekler.</span><span class="sxs-lookup"><span data-stu-id="7d965-124">Next, AddAsync serializes your key and value objects to byte arrays and appends these byte arrays to a log file on the local node.</span></span> <span data-ttu-id="7d965-125">Son olarak, aynı anahtar/değer bilgilere sahip oldukları için AddAsync bayt dizileri ikincil çoğaltmalar için gönderir.</span><span class="sxs-lookup"><span data-stu-id="7d965-125">Finally, AddAsync sends the byte arrays to all the secondary replicas so they have the same key/value information.</span></span> <span data-ttu-id="7d965-126">Anahtar/değer bilgilerini bir günlük dosyası için yazılmış olsa bile, ile ilişkili işlem kaydedilene kadar bilgileri sözlük parçası olarak kabul edilmez.</span><span class="sxs-lookup"><span data-stu-id="7d965-126">Even though the key/value information has been written to a log file, the information is not considered part of the dictionary until the transaction that they are associated with has been committed.</span></span>

<span data-ttu-id="7d965-127">Yukarıdaki kod CommitAsync çağrısı tüm işlemdeki işlemlerini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="7d965-127">In the code above, the call to CommitAsync commits all of the transaction’s operations.</span></span> <span data-ttu-id="7d965-128">Özellikle, yerel düğümdeki günlük dosyasına kayıt bilgilerini ekler ve ayrıca ikincil çoğaltmalar için yürütme kaydı gönderir.</span><span class="sxs-lookup"><span data-stu-id="7d965-128">Specifically, it appends commit information to the log file on the local node and also sends the commit record to all the secondary replicas.</span></span> <span data-ttu-id="7d965-129">Bir çoğaltma çekirdek (çoğunluğu) vermiş sonra tüm veri değişiklikleri kalıcı olarak kabul edilir ve diğer iş parçacıkları/işlemleri aynı anahtarlar işleyebileceğiniz şekilde ITransaction nesnesi yönetilebilir anahtarlarla ilişkili tüm kilitler serbest bırakılana ve bunların değerler.</span><span class="sxs-lookup"><span data-stu-id="7d965-129">Once a quorum (majority) of the replicas has replied, all data changes are considered permanent and any locks associated with keys that were manipulated via the ITransaction object are released so other threads/transactions can manipulate the same keys and their values.</span></span>

<span data-ttu-id="7d965-130">CommitAsync (oluşturulan genellikle bir özel durum nedeniyle) çağrılmazsa ITransaction nesne atıldı.</span><span class="sxs-lookup"><span data-stu-id="7d965-130">If CommitAsync is not called (usually due to an exception being thrown), then the ITransaction object gets disposed.</span></span> <span data-ttu-id="7d965-131">Service Fabric kaydedilmemiş ITransaction nesneyi atma, iptal bilgileri yerel düğümün günlük dosyasına ekler. ve hiçbir şey ikincil çoğaltmaları birine gönderilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d965-131">When disposing an uncommitted ITransaction object, Service Fabric appends abort information to the local node’s log file and nothing needs to be sent to any of the secondary replicas.</span></span> <span data-ttu-id="7d965-132">Ve daha sonra işlem yönetilebilir anahtarlarla ilişkili kilitleri serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="7d965-132">And then, any locks associated with keys that were manipulated via the transaction are released.</span></span>

## <a name="common-pitfalls-and-how-to-avoid-them"></a><span data-ttu-id="7d965-133">Ortak Tuzaklar ve bunları önleme</span><span class="sxs-lookup"><span data-stu-id="7d965-133">Common pitfalls and how to avoid them</span></span>
<span data-ttu-id="7d965-134">Güvenilir koleksiyonları dahili olarak nasıl çalıştığını anlamak, bazı ortak misuses bunların bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="7d965-134">Now that you understand how the reliable collections work internally, let’s take a look at some common misuses of them.</span></span> <span data-ttu-id="7d965-135">Aşağıdaki kodu bakın:</span><span class="sxs-lookup"><span data-stu-id="7d965-135">See the code below:</span></span>

```csharp
using (ITransaction tx = StateManager.CreateTransaction()) {
   // AddAsync serializes the name/user, logs the bytes,
   // & sends the bytes to the secondary replicas.
   await m_dic.AddAsync(tx, name, user);

   // The line below updates the property’s value in memory only; the
   // new value is NOT serialized, logged, & sent to secondary replicas.
   user.LastLogin = DateTime.UtcNow;  // Corruption!

   await tx.CommitAsync();
}
```

<span data-ttu-id="7d965-136">Normal bir .NET sözlüğü ile çalışırken, bir anahtar/değer sözlüğe ekleyin ve sonra (örneğin, LastLogin) bir özelliğin değerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7d965-136">When working with a regular .NET dictionary, you can add a key/value to the dictionary and then change the value of a property (such as LastLogin).</span></span> <span data-ttu-id="7d965-137">Ancak, bu kod ile güvenilir bir sözlük düzgün çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="7d965-137">However, this code will not work correctly with a reliable dictionary.</span></span> <span data-ttu-id="7d965-138">Unutmayın önceki tartışma AddAsync çağrısı bayt dizileri anahtar/değer nesnelere serileştirir ve ardından diziler yerel bir dosyaya kaydeder ve aynı zamanda ikincil çoğaltmalar için gönderir.</span><span class="sxs-lookup"><span data-stu-id="7d965-138">Remember from the earlier discussion, the call to AddAsync serializes the key/value objects to byte arrays and then saves the arrays to a local file and also sends them to the secondary replicas.</span></span> <span data-ttu-id="7d965-139">Bir özellik daha sonra değiştirirseniz, bu özelliğin değeri yalnızca bellekte değiştirir; Yerel dosya veya çoğaltmalar için gönderilen verileri etkilemez.</span><span class="sxs-lookup"><span data-stu-id="7d965-139">If you later change a property, this changes the property’s value in memory only; it does not impact the local file or the data sent to the replicas.</span></span> <span data-ttu-id="7d965-140">İşlem çökerse bellekte nedir hemen atılır.</span><span class="sxs-lookup"><span data-stu-id="7d965-140">If the process crashes, what’s in memory is thrown away.</span></span> <span data-ttu-id="7d965-141">Yeni bir işlem başlatıldığında veya başka bir çoğaltma birincil hale gelirse, eski özellik değeri kullanılabilir olduğu.</span><span class="sxs-lookup"><span data-stu-id="7d965-141">When a new process starts or if another replica becomes primary, then the old property value is what is available.</span></span>

<span data-ttu-id="7d965-142">Yeterli ne kadar kolay yukarıda gösterilen hata türü yapma olduğunu stres olamaz.</span><span class="sxs-lookup"><span data-stu-id="7d965-142">I cannot stress enough how easy it is to make the kind of mistake shown above.</span></span> <span data-ttu-id="7d965-143">Ve işlem arıza hakkında hata IF/olduğunda yalnızca öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="7d965-143">And, you will only learn about the mistake if/when the process goes down.</span></span> <span data-ttu-id="7d965-144">Doğru bir şekilde kod yazmaya iki satırları tersine çevirmek için basitçe verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7d965-144">The correct way to write the code is simply to reverse the two lines:</span></span>


```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   user.LastLogin = DateTime.UtcNow;  // Do this BEFORE calling AddAsync
   await m_dic.AddAsync(tx, name, user);
   await tx.CommitAsync();
}
```

<span data-ttu-id="7d965-145">Aşağıda, bir ortak hata gösteren başka bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7d965-145">Here is another example showing a common mistake:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use the user’s name to look up their data
   ConditionalValue<User> user =
      await m_dic.TryGetValueAsync(tx, name);

   // The user exists in the dictionary, update one of their properties.
   if (user.HasValue) {
      // The line below updates the property’s value in memory only; the
      // new value is NOT serialized, logged, & sent to secondary replicas.
      user.Value.LastLogin = DateTime.UtcNow; // Corruption!
      await tx.CommitAsync();
   }
}
```

<span data-ttu-id="7d965-146">Yeniden normal .NET sözlükler, yukarıdaki kod düzgün çalışır ve ortak bir desen: geliştirici bir değeri aramak için bir anahtar kullanır.</span><span class="sxs-lookup"><span data-stu-id="7d965-146">Again, with regular .NET dictionaries, the code above works fine and is a common pattern: the developer uses a key to look up a value.</span></span> <span data-ttu-id="7d965-147">Değeri varsa, geliştirici bir özelliğin değerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="7d965-147">If the value exists, the developer changes a property’s value.</span></span> <span data-ttu-id="7d965-148">Ancak, güvenilir koleksiyonlarla bu kodu zaten ele alınan aynı sorunun yaşandığı: **güvenilir bir koleksiyona verdiğiniz sonra bir nesne değiştirmemelisiniz.**</span><span class="sxs-lookup"><span data-stu-id="7d965-148">However, with reliable collections, this code exhibits the same problem as already discussed: **you MUST not modify an object once you have given it to a reliable collection.**</span></span>

<span data-ttu-id="7d965-149">Güvenilir bir koleksiyonda bir değer güncelleştirmek için doğru bir şekilde olan mevcut değeri bir başvuru almak ve bu başvuru değişmez tarafından başvurulan nesne göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="7d965-149">The correct way to update a value in a reliable collection, is to get a reference to the existing value and consider the object referred to by this reference immutable.</span></span> <span data-ttu-id="7d965-150">Ardından, özgün nesne tam bir kopyası olan yeni bir nesne oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7d965-150">Then, create a new object which is an exact copy of the original object.</span></span> <span data-ttu-id="7d965-151">Şimdi, bu yeni nesnenin durumunu değiştirin ve yeni koleksiyon nesnesine bayt dizileri için serileştirilir böylece yerel dosyanın sonuna ve çoğaltmalar için gönderilen yazma.</span><span class="sxs-lookup"><span data-stu-id="7d965-151">Now, you can modify the state of this new object and write the new object into the collection so that it gets serialized to byte arrays, appended to the local file and sent to the replicas.</span></span> <span data-ttu-id="7d965-152">Değişiklikler yaptıktan sonra bellek içi nesneleri, yerel dosya ve tüm çoğaltmaların aynı tam olarak aynı durum vardır.</span><span class="sxs-lookup"><span data-stu-id="7d965-152">After committing the change(s), the in-memory objects, the local file, and all the replicas have the same exact state.</span></span> <span data-ttu-id="7d965-153">Tüm iyi!</span><span class="sxs-lookup"><span data-stu-id="7d965-153">All is good!</span></span>

<span data-ttu-id="7d965-154">Aşağıdaki kod, güvenilir bir koleksiyonda bir değer güncelleştirmek için doğru bir şekilde gösterir:</span><span class="sxs-lookup"><span data-stu-id="7d965-154">The code below shows the correct way to update a value in a reliable collection:</span></span>

```csharp

using (ITransaction tx = StateManager.CreateTransaction()) {
   // Use the user’s name to look up their data
   ConditionalValue<User> currentUser =
      await m_dic.TryGetValueAsync(tx, name);

   // The user exists in the dictionary, update one of their properties.
   if (currentUser.HasValue) {
      // Create new user object with the same state as the current user object.
      // NOTE: This must be a deep copy; not a shallow copy. Specifically, only
      // immutable state can be shared by currentUser & updatedUser object graphs.
      User updatedUser = new User(currentUser);

      // In the new object, modify any properties you desire
      updatedUser.LastLogin = DateTime.UtcNow;

      // Update the key’s value to the updateUser info
      await m_dic.SetValue(tx, name, updatedUser);

      await tx.CommitAsync();
   }
}
```

## <a name="define-immutable-data-types-to-prevent-programmer-error"></a><span data-ttu-id="7d965-155">Programcı hatayı önlemek için sabit veri türlerini tanımlayın</span><span class="sxs-lookup"><span data-stu-id="7d965-155">Define immutable data types to prevent programmer error</span></span>
<span data-ttu-id="7d965-156">İdeal olarak, yanlışlıkla değişmez göz önünde bulundurmanız gereken bir nesnenin durumu değiştirdiği kod üretmek zaman derleyici hatalarını raporlamak isteriz.</span><span class="sxs-lookup"><span data-stu-id="7d965-156">Ideally, we’d like the compiler to report errors when you accidentally produce code that mutates state of an object that you are supposed to consider immutable.</span></span> <span data-ttu-id="7d965-157">Ancak, C# Derleyici bunu olanağına sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="7d965-157">But, the C# compiler does not have the ability to do this.</span></span> <span data-ttu-id="7d965-158">Bu nedenle, olası Programcı hataları önlemek için türlerden tanımladığınız öneririz değişmez tür için güvenilir koleksiyonlarla kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d965-158">So, to avoid potential programmer bugs, we highly recommend that you define the types you use with reliable collections to be immutable types.</span></span> <span data-ttu-id="7d965-159">Bu özellikle, çekirdek değer türleri (örneğin, numaraları [Int32, UInt64, vb.], DateTime, Guid, TimeSpan ve benzeri) için takılıyor anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7d965-159">Specifically, this means that you stick to core value types (such as numbers [Int32, UInt64, etc.], DateTime, Guid, TimeSpan, and the like).</span></span> <span data-ttu-id="7d965-160">Ve tabi ki, ayrıca dize kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d965-160">And, of course, you can also use String.</span></span> <span data-ttu-id="7d965-161">Seri hale getirme olarak koleksiyon özellikleri önlemek en iyisidir ve bunları seri durumdan sık performansa zarar verebilir.</span><span class="sxs-lookup"><span data-stu-id="7d965-161">It is best to avoid collection properties as serializing and deserializing them can frequently can hurt performance.</span></span> <span data-ttu-id="7d965-162">Ancak, koleksiyon özellikleri kullanmak istiyorsanız, yüksek oranda kullanılmasını öneririz. NET'in değişmez koleksiyonlar kitaplığı ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span><span class="sxs-lookup"><span data-stu-id="7d965-162">However, if you want to use collection properties, we highly recommend the use of .NET’s immutable collections library ([System.Collections.Immutable](https://www.nuget.org/packages/System.Collections.Immutable/)).</span></span> <span data-ttu-id="7d965-163">Bu kitaplık http://nuget.org karşıdan yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="7d965-163">This library is available for download from http://nuget.org.</span></span> <span data-ttu-id="7d965-164">Ayrıca, sınıflarınızı mühürleme ve mümkün olduğunda alanları salt okunur yapma öneririz.</span><span class="sxs-lookup"><span data-stu-id="7d965-164">We also recommend sealing your classes and making fields read-only whenever possible.</span></span>

<span data-ttu-id="7d965-165">Aşağıdaki kullanıcı bilgisi türünü, daha önce bahsedilen önerileri yararlanarak bir sabit türü tanımlamak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7d965-165">The UserInfo type below demonstrates how to define an immutable type taking advantage of aforementioned recommendations.</span></span>

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
      // Convert the deserialized collection to an immutable collection
      ItemsBidding = ItemsBidding.ToImmutableList();
   }

   [DataMember]
   public readonly String Email;

   // Ideally, this would be a readonly field but it can't be because OnDeserialized
   // has to set it. So instead, the getter is public and the setter is private.
   [DataMember]
   public IEnumerable<ItemId> ItemsBidding { get; private set; }

   // Since each UserInfo object is immutable, we add a new ItemId to the ItemsBidding
   // collection by creating a new immutable UserInfo object with the added ItemId.
   public UserInfo AddItemBidding(ItemId itemId) {
      return new UserInfo(Email, ((ImmutableList<ItemId>)ItemsBidding).Add(itemId));
   }
}
```

<span data-ttu-id="7d965-166">Öğe kimliği türü ayrıca bir değişmez aşağıda gösterildiği gibi türüdür:</span><span class="sxs-lookup"><span data-stu-id="7d965-166">The ItemId type is also an immutable type as shown here:</span></span>

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

## <a name="schema-versioning-upgrades"></a><span data-ttu-id="7d965-167">Şema sürüm oluşturma (yükseltme)</span><span class="sxs-lookup"><span data-stu-id="7d965-167">Schema versioning (upgrades)</span></span>
<span data-ttu-id="7d965-168">Dahili olarak, güvenilir koleksiyonları kullanarak nesnelerinizin seri hale. NET'in DataContractSerializer.</span><span class="sxs-lookup"><span data-stu-id="7d965-168">Internally, Reliable Collections serialize your objects using .NET’s DataContractSerializer.</span></span> <span data-ttu-id="7d965-169">Serileştirilmiş nesneler birincil kopyanın yerel diske yazılır ve ikincil çoğaltmalar için de iletilir.</span><span class="sxs-lookup"><span data-stu-id="7d965-169">The serialized objects are persisted to the primary replica’s local disk and are also transmitted to the secondary replicas.</span></span> <span data-ttu-id="7d965-170">Hizmetinizi geliştikçe hizmetiniz için gerekli verileri (şema) türünü değiştirmek istersiniz olasıdır.</span><span class="sxs-lookup"><span data-stu-id="7d965-170">As your service matures, it’s likely you’ll want to change the kind of data (schema) your service requires.</span></span> <span data-ttu-id="7d965-171">Sürüm oluşturma dikkatli verilerinizin yaklaşımını gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d965-171">You must approach versioning of your data with great care.</span></span> <span data-ttu-id="7d965-172">Öncelikle, her zaman eski verileri seri durumdan mümkün olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d965-172">First and foremost, you must always be able to deserialize old data.</span></span> <span data-ttu-id="7d965-173">Özellikle, bu seri durumdan çıkarma kodunuzu sonsuz geriye dönük olarak uyumlu olmalıdır anlamına gelir: sürüm 333 service kodunuzun sağlayabilmelidir güvenilir bir koleksiyonda 5 yıl önce hizmet kodunuzun 1 sürümü tarafından yerleştirilen veriler üzerinde işlem yaparsınız.</span><span class="sxs-lookup"><span data-stu-id="7d965-173">Specifically, this means your deserialization code must be infinitely backward compatible: Version 333 of your service code must be able to operate on data placed in a reliable collection by version 1 of your service code 5 years ago.</span></span>

<span data-ttu-id="7d965-174">Ayrıca, hizmet yükseltilen bir yükseltme etki alanı aynı anda kodudur.</span><span class="sxs-lookup"><span data-stu-id="7d965-174">Furthermore, service code is upgraded one upgrade domain at a time.</span></span> <span data-ttu-id="7d965-175">Bu nedenle, yükseltme sırasında hizmet kodunuzun eşzamanlı çalışan iki farklı sürümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d965-175">So, during an upgrade, you have two different versions of your service code running simultaneously.</span></span> <span data-ttu-id="7d965-176">Hizmet kodunuzu yeni sürümünü service kodunuzun eski sürümlerini yeni şema işlemek olmayabilir olarak yeni şemayı kullanmak zorunda kalmamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d965-176">You must avoid having the new version of your service code use the new schema as old versions of your service code might not be able to handle the new schema.</span></span> <span data-ttu-id="7d965-177">Mümkün olduğunda, her sürüm 1 sürümü tarafından ileri doğru uyumlu olacak şekilde hizmetinizin tasarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d965-177">When possible, you should design each version of your service to be forward compatible by 1 version.</span></span> <span data-ttu-id="7d965-178">Özellikle, bu hizmet kodunuzun V1 yalnızca açıkça işlemiyor hiçbir şema öğeleri yoksay mümkün olması anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7d965-178">Specifically, this means that V1 of your service code should be able to simply ignore any schema elements it does not explicitly handle.</span></span> <span data-ttu-id="7d965-179">Ancak, herhangi bir veri açıkça hakkında bilmiyor ve yalnızca geri çıkışı bir sözlük anahtar veya değer güncelleştirilirken yazma kaydedemediğini olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d965-179">However, it must be able to save any data it doesn’t explicitly know about and simply write it back out when updating a dictionary key or value.</span></span>

> [!WARNING]
> <span data-ttu-id="7d965-180">Bir anahtar şeması değiştirebilirsiniz, ancak, anahtarın karma kodu ve eşittir algoritmaları kararlı olduğundan emin olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="7d965-180">While you can modify the schema of a key, you must ensure that your key’s hash code and equals algorithms are stable.</span></span> <span data-ttu-id="7d965-181">Bu algoritmalar birini nasıl çalıştığını değiştirirseniz, anahtarı güvenilir sözlük içinde herhangi bir zamanda yeniden aramak mümkün olmaz.</span><span class="sxs-lookup"><span data-stu-id="7d965-181">If you change how either of these algorithms operate, you will not be able to look up the key within the reliable dictionary ever again.</span></span>
>
>

<span data-ttu-id="7d965-182">Alternatif olarak, ne genellikle 2 aşamalı yükseltme olarak bilinir gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d965-182">Alternatively, you can perform what is typically referred to as a 2-phase upgrade.</span></span> <span data-ttu-id="7d965-183">Aşama 2 yükseltme işlemine hizmetinizi V1 ile V2'ye yükseltme: V2 kodunu içerir, yeni şema değişikliği dağıtılacak bildiği ancak bu kodu yürütmez.</span><span class="sxs-lookup"><span data-stu-id="7d965-183">With a 2-phase upgrade, you upgrade your service from V1 to V2: V2 contains the code that knows how to deal with the new schema change but this code doesn’t execute.</span></span> <span data-ttu-id="7d965-184">V2 kod V1 veri okuduğunda üzerinde çalışır ve V1 verileri yazar.</span><span class="sxs-lookup"><span data-stu-id="7d965-184">When the V2 code reads V1 data, it operates on it and writes V1 data.</span></span> <span data-ttu-id="7d965-185">Tüm yükseltme etki alanları arasında yükseltme tamamlandıktan sonra daha sonra şekilde çalışan V2 örneklerini yükseltme tamamlandıktan sinyal.</span><span class="sxs-lookup"><span data-stu-id="7d965-185">Then, after the upgrade is complete across all upgrade domains, you can somehow signal to the running V2 instances that the upgrade is complete.</span></span> <span data-ttu-id="7d965-186">(Tek yönlü sinyal için bu yapılandırma yükseltme alma; Bu aşama 2 yükseltme bunu yapar.) Şimdi, V2 örnekleri V1 veri okuma, V2 veriye dönüştürme, üzerinde çalışır ve V2 verileri olarak yazamadı.</span><span class="sxs-lookup"><span data-stu-id="7d965-186">(One way to signal this is to roll out a configuration upgrade; this is what makes this a 2-phase upgrade.) Now, the V2 instances can read V1 data, convert it to V2 data, operate on it, and write it out as V2 data.</span></span> <span data-ttu-id="7d965-187">Diğer örnekleri V2 verileri okurken dönüştürmeden zorunda değildir, bunlar yalnızca üzerinde çalışır ve V2 verileri yazma.</span><span class="sxs-lookup"><span data-stu-id="7d965-187">When other instances read V2 data, they do not need to convert it, they just operate on it, and write out V2 data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d965-188">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="7d965-188">Next Steps</span></span>
<span data-ttu-id="7d965-189">İleri uyumlu veri sözleşmeleri oluşturma hakkında bilgi edinmek için [İleri uyumlu veri sözleşmeleri](https://msdn.microsoft.com/library/ms731083.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d965-189">To learn about creating forward compatible data contracts, see [Forward-Compatible Data Contracts](https://msdn.microsoft.com/library/ms731083.aspx).</span></span>

<span data-ttu-id="7d965-190">Sürüm veri sözleşmelerinde en iyi yöntemleri öğrenmek için bkz: [veri sözleşmesi sürümü oluşturma](https://msdn.microsoft.com/library/ms731138.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d965-190">To learn best practices on versioning data contracts, see [Data Contract Versioning](https://msdn.microsoft.com/library/ms731138.aspx).</span></span>

<span data-ttu-id="7d965-191">Sürüm dayanıklı veri sözleşmeleri uygulamak öğrenmek için bkz: [sürüm toleranslı seri hale getirme geri çağrıları](https://msdn.microsoft.com/library/ms733734.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d965-191">To learn how to implement version tolerant data contracts, see [Version-Tolerant Serialization Callbacks](https://msdn.microsoft.com/library/ms733734.aspx).</span></span>

<span data-ttu-id="7d965-192">Birden çok sürümleri arasında çalışabilirler bir veri yapısını sağlamak öğrenmek için bkz: [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span><span class="sxs-lookup"><span data-stu-id="7d965-192">To learn how to provide a data structure that can interoperate across multiple versions, see [IExtensibleDataObject](https://msdn.microsoft.com/library/system.runtime.serialization.iextensibledataobject.aspx).</span></span>
