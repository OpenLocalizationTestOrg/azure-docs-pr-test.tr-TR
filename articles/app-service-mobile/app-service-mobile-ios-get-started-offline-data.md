---
title: "iOS mobil uygulamaları ile aaaEnable çevrimdışı eşitleme | Microsoft Docs"
description: "Bilgi nasıl toouse Azure App Service mobile apps toocache ve eşitleme çevrimdışı verileri iOS uygulamaları."
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: eb5b9520-0f39-4a09-940a-dadb6d940db8
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 570ea7cf6694ab7317c977331038929b64508ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-syncing-with-ios-mobile-apps"></a>Çevrimdışı iOS mobil uygulamaları ile eşitlemeyi etkinleştir
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici, iOS için Azure App Service'in hello Mobile Apps özelliğini çevrimdışı eşitleme kapsar. Çevrimdışı eşitleme son kullanıcılar ile mobil uygulama tooview ile etkileşim, ekleyin veya bile ağ bağlantısı olduğunda veri değiştirin. Değişiklikler yerel bir veritabanında depolanır. Merhaba cihaz yeniden çevrimiçi olduktan sonra hello değişiklikler hello uzak arka ucu ile eşitlenir.

Mobile Apps ile ilk deneyiminizi varsa hello öğretici ilk tamamlanmalıdır [iOS uygulaması oluştur]. Merhaba indirilen hızlı başlangıç sunucu projesi kullanmazsanız hello veri erişimi uzantı paketleri tooyour projesi eklemeniz gerekir. Server uzantısı paketleri hakkında daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

toolearn hello çevrimdışı eşitleme özelliği hakkında daha fazla bilgi görmek [mobil uygulamalarda çevrimdışı veri eşitlemeye].

## <a name="review-sync"></a>Merhaba istemci eşitleme kodu gözden geçirme
Merhaba indirdiğiniz hello istemci projesi [iOS uygulaması oluştur] öğretici zaten bir yerel çekirdek veri tabanlı veritabanı çevrimdışı eşitlemeyi destekleyen kodunu içerir. Bu bölümde hello Eğitmen kodu zaten dahil özetlenmektedir. Merhaba özelliği kavramsal bir genel bakış için bkz: [mobil uygulamalarda çevrimdışı veri eşitlemeye].

Merhaba ağ erişilemez durumda olduğunda bile Mobile Apps hello çevrimdışı veri eşitleme özelliğini kullanarak, son kullanıcılar ile yerel bir veritabanı etkileşimli olarak çalışabilir. toouse bu özellikler, uygulamanızda hello eşitleme bağlamı başlatma `MSClient` ve yerel bir depo başvuru. Tablonuz hello aracılığıyla başvuru sonra **MSSyncTable** arabirimi.

İçinde **QSTodoService.m** (Objective-C) veya **ToDoTableViewController.swift** hello üye türü hello (Swift), bildirim **syncTable** olan  **MSSyncTable**. Çevrimdışı eşitleme kullanan bu eşitleme tablo arabirimi yerine **MSTable**. Bir eşitleme tablo kullanıldığında, tüm işlemleri yalnızca uzak arka uç açık itme hello eşitlendiğini toohello yerel deposu gidin ve işlemleri çekme.

 tooget bir başvuru tooa eşitleme tablosu kullanmak hello **syncTableWithName** yöntemi `MSClient`. tooremove çevrimdışı eşitleme işlevselliği, kullanım **tableWithName** yerine.

Tablo işlemleri gerçekleştirilmeden önce hello yerel depolama başlatılmalıdır. Merhaba ilgili kod aşağıdadır:

* **Objective-C**. Merhaba, **QSTodoService.init** yöntemi:

   ```objc
   MSCoreDataStore *store = [[MSCoreDataStore alloc] initWithManagedObjectContext:context];
   self.client.syncContext = [[MSSyncContext alloc] initWithDelegate:nil dataSource:store callback:nil];
   ```    
* **SWIFT**. Merhaba, **ToDoTableViewController.viewDidLoad** yöntemi:

   ```swift
   let client = MSClient(applicationURLString: "http:// ...") // URI of hello Mobile App
   let managedObjectContext = (UIApplication.sharedApplication().delegate as! AppDelegate).managedObjectContext!
   self.store = MSCoreDataStore(managedObjectContext: managedObjectContext)
   client.syncContext = MSSyncContext(delegate: nil, dataSource: self.store, callback: nil)
   ```
   Bu yöntem hello kullanarak yerel bir depo oluşturur `MSCoreDataStore` Mobile Apps SDK'sı hello arabirim sağlar. Merhaba uygulayarak farklı bir yerel deposu alternatif olarak, sağlayabilir `MSSyncContextDataSource` protokolü. Ayrıca, ilk parametresinin hello **MSSyncContext** kullanılan toospecify çakışma işleyicisidir. Biz başarılı olduğundan `nil`, biz üzerinde herhangi bir çakışmanın başarısız hello varsayılan çakışma işleyici alın.

Şimdi, şimdi hello gerçek eşitleme işlemi gerçekleştirmek ve verileri hello uzak arka uçtan alın:

* **Objective-C**. `syncData`Yeni değişiklikler ilk iter ve çağırır **pullData** hello uzak arka uçtan tooget veri. Buna karşılık, hello **pullData** yöntemi bir sorguyla eşleşen yeni verileri alır:

   ```objc
   -(void)syncData:(QSCompletionBlock)completion
   {
       // Push all changes in hello sync context, and then pull new data.
       [self.client.syncContext pushWithCompletion:^(NSError *error) {
           [self logErrorIfNotNil:error];
           [self pullData:completion];
       }];
   }

   -(void)pullData:(QSCompletionBlock)completion
   {
       MSQuery *query = [self.syncTable query];

       // Pulls data from hello remote server into hello local table.
       // We're pulling all items and filtering in hello view.
       // Query ID is used for incremental sync.
       [self.syncTable pullWithQuery:query queryId:@"allTodoItems" completion:^(NSError *error) {
           [self logErrorIfNotNil:error];

           // Lets hello caller know that we have finished.
           if (completion != nil) {
               dispatch_async(dispatch_get_main_queue(), completion);
           }
       }];
   }
   ```
* **SWIFT**:
   ```swift
   func onRefresh(sender: UIRefreshControl!) {
      UIApplication.sharedApplication().networkActivityIndicatorVisible = true

      self.table!.pullWithQuery(self.table?.query(), queryId: "AllRecords") {
          (error) -> Void in

          UIApplication.sharedApplication().networkActivityIndicatorVisible = false

          if error != nil {
              // A real application would handle various errors like network conditions,
              // server conflicts, etc via hello MSSyncContextDelegate
              print("Error: \(error!.description)")

              // We will discard our changes and keep hello server's copy for simplicity
              if let opErrors = error!.userInfo[MSErrorPushResultKey] as? Array<MSTableOperationError> {
                  for opError in opErrors {
                      print("Attempted operation tooitem \(opError.itemId)")
                      if (opError.operation == .Insert || opError.operation == .Delete) {
                          print("Insert/Delete, failed discarding changes")
                          opError.cancelOperationAndDiscardItemWithCompletion(nil)
                      } else {
                          print("Update failed, reverting tooserver's copy")
                          opError.cancelOperationAndUpdateItem(opError.serverItem!, completion: nil)
                      }
                  }
              }
          }
          self.refreshControl?.endRefreshing()
      }
   }
   ```

Merhaba Objective-C sürümünde, içinde `syncData`, ilk diyoruz **pushWithCompletion** üzerinde hello eşitleme bağlamı. Bu yöntem bir üyesi olan `MSSyncContext` (ve hello eşitleme tablonun kendisini değil) tüm tablolar arasında değişiklikleri iter olduğundan. Yerel olarak (CUD işlemleri üzerinden) şekilde değiştirilmiş kayıtları toohello sunucu gönderilir. Yardımcı hello **pullData** çağrıldığında hangi çağrıları **MSSyncTable.pullWithQuery** tooretrieve uzak veri ve hello yerel veritabanında depolar.

Merhaba SWIFT sürümünde hello gönderme işlemi kesinlikle gerekli olmadığından yoktur çağrı yok çok**pushWithCompletion**. Gönderme işlemi yapıyor Merhaba tablonun hello eşitleme bağlamındaki bekleyen tüm değişiklikleri varsa, çekme her zaman bir itme ilk verir. Ancak, birden fazla eşitleme tablo varsa, en iyi tooexplicitly çağrı anında tooensure her şeyi ilişkili tablolar arasında tutarlı olduğundan emin olur.

Merhaba Objective-C hem SWIFT sürümleri hello kullanabilirsiniz **pullWithQuery** yöntemi toospecify sorgu toofilter hello tooretrieve istediğiniz kaydeder. Bu örnekte, hello sorgu hello uzak tüm kayıtları alır `TodoItem` tablo.

ikinci parametresi, hello **pullWithQuery** için kullanılan bir sorgu kimliği *Artımlı eşitleme*. Artımlı eşitleme hello kaydın kullanarak hello son eşitlemeden sonra değiştirilen kayıtları alır `UpdatedAt` zaman damgası (adlı `updatedAt` hello yerel depolama alanındaki) hello sorgu kimliği her mantıksal sorgu için benzersiz tanımlayıcı bir dize olmalıdır Uygulamanızı. tooopt Artımlı eşitleme dışına geçirmek `nil` sorgu kimliği hello gibi Her çekme işlemi tüm kayıtları aldığı için bu yaklaşım olası verimsiz olabilir.

Merhaba Objective-C uygulama değiştirmek veya bir kullanıcı hello yenileme hareketi gerçekleştirdiğinde veri eklediğinizde ve başlatma eşitlenir.

Merhaba SWIFT uygulama hello kullanıcı hello yenileme hareketi gerçekleştirdiğinde ve başlatma eşitlenir.

Merhaba veri olduğunda uygulama eşitlemeler (Objective-C) değiştirdiğinden ya da hello uygulama (Objective-C ve Swift) başlattığında hello uygulama hello kullanıcının çevrimiçi olduğunu varsayar. Sonraki bölümde, böylece kullanıcılar çevrimdışı olsalar bile düzenleyebilirsiniz hello uygulamayı güncelleştirir.

## <a name="review-core-data"></a>Gözden geçirme hello çekirdek veri modeli
Merhaba çekirdek veri çevrimdışı deposu kullandığınızda, veri modelinizi belirli tabloları ve alanları tanımlamanız gerekir. Merhaba örnek uygulaması zaten hello doğru biçime sahip bir veri modeli içerir. Bu bölümde, nasıl kullanıldıkları Biz bu tablolar tooshow yol.

Açık **QSDataModel.xcdatamodeld**. Dört tablolar tanımlanan--tarafından kullanılan üç SDK hello ve hello Yapılacaklar için kullanılan bir öğelerini kendilerini:
  * MS_TableOperations: Parçaları toobe hello eşitlenmesi gereken öğeleri hello.
  * MS_TableOperationErrors: Çevrimdışı eşitleme sırasında gerçekleşen hataları izler.
  * MS_TableConfig: Hello son eşitleme işlemi tüm çekme işlemleri için güncelleştirilmiş son kez parçaları hello.
  * Todoıtem: hello Yapılacaklar öğelerini depolar. Sistem sütunları hello **createdAt**, **updatedAt**, ve **sürüm** isteğe bağlı sistem özelliklerdir.

> [!NOTE]
> Merhaba Mobile Apps SDK'sı ile başlayan sütun adları ayırır "**``**". Bu ön ek sistem sütunlar dışındaki herhangi bir şeyle kullanmayın. Aksi takdirde hello uzak arka uç kullandığınızda, sütun adlarının değiştirilir.
>
>

Merhaba çevrimdışı eşitleme özelliğini kullandığınızda, hello üç Sistem tabloları ve hello veri tablosu tanımlayın.

### <a name="system-tables"></a>Sistem tabloları

**MS_TableOperations**  

![MS_TableOperations tablo öznitelikleri][defining-core-data-tableoperations-entity]

| Öznitelik | Tür |
| --- | --- |
| id | Tamsayı 64 |
| öğe kimliği | Dize |
| properties | İkili veriler |
| Tablo | Dize |
| tableKind | Tamsayı 16 |


**MS_TableOperationErrors**

 ![MS_TableOperationErrors tablo öznitelikleri][defining-core-data-tableoperationerrors-entity]

| Öznitelik | Tür |
| --- | --- |
| id |Dize |
| Operationıd |Tamsayı 64 |
| properties |İkili veriler |
| tableKind |Tamsayı 16 |

 **MS_TableConfig**

 ![][defining-core-data-tableconfig-entity]

| Öznitelik | Tür |
| --- | --- |
| id |Dize |
| anahtar |Dize |
| keyType |Tamsayı 64 |
| Tablo |Dize |
| değer |Dize |

### <a name="data-table"></a>Veri tablosu

**Todoıtem**

| Öznitelik | Tür | Not |
| --- | --- | --- |
| id | Dize, gerekli olarak işaretlenmiş |Uzak Depolama birincil anahtar |
| Tamamlayın | Boole değeri | Yapılacak iş öğesi alanı |
| Metin |Dize |Yapılacak iş öğesi alanı |
| CreatedAt | Tarih | (isteğe bağlı) Çok eşlemeleri**createdAt** sistem özelliği |
| updatedAt | Tarih | (isteğe bağlı) Çok eşlemeleri**updatedAt** sistem özelliği |
| Sürüm | Dize | (isteğe bağlı) Kullanılan toodetect çakışmaları, maps tooversion |

## <a name="setup-sync"></a>Hello uygulama Hello eşitleme davranışını değiştirme
Bu bölümde, uygulama başlatma ya da zaman eklemek ve öğeleri güncelleştirme üzerinde eşitlemez şekilde hello uygulama değiştirin. Yalnızca hello Yenile hareketi düğmesini gerçekleştirildiğinde eşitlenir.

**Objective-C**:

1. İçinde **QSTodoListViewController.m**, hello değiştirme **viewDidLoad** yöntemi tooremove hello çağrısı çok`[self refresh]` hello yöntemi hello sonunda. Şimdi, uygulama başlatılırken hello sunucusuyla hello veri eşitlenmedi. Bunun yerine, hello yerel deposunun Merhaba içeriğine ile eşitlenip.
2. İçinde **QSTodoService.m**, hello tanımını değiştirmek `addItem` böylece hello öğesi eklendikten sonra eşitleme değil. Merhaba kaldırmak `self syncData` engelleme ve hello şununla değiştirin:

   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```
3. Merhaba tanımını değiştirmek `completeItem` daha önce belirtildiği gibi. Başlangıç engellemeyi kaldırmak `self syncData` ve hello şununla değiştirin:
   ```objc
   if (completion != nil) {
       dispatch_async(dispatch_get_main_queue(), completion);
   }
   ```

**SWIFT**:

İçinde `viewDidLoad`, **ToDoTableViewController.swift**, burada, app başlangıç eşitleniyor toostop gösterilen hello iki satırları açıklama. Bu yazma hello anda birisi ekler veya öğeyi tamamlandıktan hello Swift Todo uygulaması hello hizmet güncelleştirmez. Merhaba hizmeti yalnızca, uygulama başlatılırken güncelleştirir.

   ```swift
  self.refreshControl?.beginRefreshing()
  self.onRefresh(self.refreshControl)
```

## <a name="test-app"></a>Test hello uygulama
Bu bölümde, tooan geçersiz URL toosimulate çevrimdışı bir senaryo bağlayın. Veri öğeleri eklediğinizde, tutulan hello Yerel Çekirdek veri depolamak, ancak bunlar hello mobil uygulama arka ucu ile eşitlenmedi.

1. Merhaba mobil uygulama URL'sini değiştirmek **QSTodoService.m** tooan geçersiz URL ve yeniden çalışma hello uygulama:

   **Objective-C**. QSTodoService.m içinde:
   ```objc
   self.client = [MSClient clientWithApplicationURLString:@"https://sitename.azurewebsites.net.fail"];
   ```
   **SWIFT**. ToDoTableViewController.swift içinde:
   ```swift
   let client = MSClient(applicationURLString: "https://sitename.azurewebsites.net.fail")
   ```
2. Bazı Yapılacaklar öğelerini ekleyin. Merhaba simulator (veya zorla kapatma hello uygulama) çıkmanız ve yeniden başlatın. Yaptığınız değişiklikleri kalıcı olduğunu doğrulayın.

3. Görüntüleme hello uzak Merhaba içeriğine **Todoıtem** tablosu:
   * Node.js arka ucu için toohello Git [Azure portal](https://portal.azure.com/) ve, mobil uygulama arka ucu içinde tıklatın **kolay tabloları** > **Todoıtem**.  
   * Bir .NET geri için sonlandırmak için SQL Server Management Studio gibi bir SQL aracı veya Fiddler veya Postman gibi bir REST istemcisi kullanın.  

4. Merhaba yeni öğelerin bulunduğunu doğrulayın *değil* edilmiş hello sunucusuyla eşitlenir.

5. Değişiklik hello URL toohello düzeltmek birinde **QSTodoService.m**ve yeniden çalıştır hello uygulama.

6. Merhaba yenileme hareketi öğeleri hello listede aşağı çekerek gerçekleştirin.  
Devam eden değer değiştirici görüntülenir.

7. Görünüm hello **Todoıtem** yeniden verileri. Merhaba yeni ve değiştirilen Yapılacaklar öğelerini şimdi görüntülenmesi gerekir.

## <a name="summary"></a>Özet
toosupport hello çevrimdışı eşitleme özelliği kullandık hello `MSSyncTable` arabirim ve başlatıldı `MSClient.syncContext` yerel deposu. Bu durumda, hello yerel deposu çekirdek veri tabanlı bir veritabanı oluştu.

Bir çekirdek veri yerel deposu kullandığınızda, hello birkaç tablolarla tanımlamalısınız [düzeltmek Sistem Özellikleri](#review-core-data).

Hello normal oluşturmak okuma, güncelleştirme ve hello uygulama hala bağlı, ancak tüm hello işlemleri hello yerel depo ortaya gibi mobil uygulamaları iş için (CRUD) işlemleridir silme.

Merhaba yerel deposu hello sunucuyla eşitlendiğinde hello kullandık **MSSyncTable.pullWithQuery** yöntemi.

## <a name="additional-resources"></a>Ek kaynaklar
* [mobil uygulamalarda çevrimdışı veri eşitlemeye]
* [Bulut kapsar: Azure Mobile Services'ın çevrimdışı eşitleme] \(hello video Mobile Services hakkında olmakla birlikte, benzer şekilde Mobile Apps çevrimdışı eşitleme çalışır.\)

<!-- URLs. -->


[iOS uygulaması oluştur]: app-service-mobile-ios-get-started.md
[mobil uygulamalarda çevrimdışı veri eşitlemeye]: app-service-mobile-offline-data-sync.md

[defining-core-data-tableoperationerrors-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperationerrors-entity.png
[defining-core-data-tableoperations-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableoperations-entity.png
[defining-core-data-tableconfig-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-tableconfig-entity.png
[defining-core-data-todoitem-entity]: ./media/app-service-mobile-ios-get-started-offline-data/defining-core-data-todoitem-entity.png

[Bulut kapsar: Azure Mobile Services'ın çevrimdışı eşitleme]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/en-us/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/
