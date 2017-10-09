
Varsayılan olarak, Mobile Apps arka uç API'leri anonim olarak çağrılabilir. Ardından, toorestrict erişim kimliği doğrulanmış tooonly istemcileri gerekir.  

* **Node.js geri bitiş (hello Azure portalı)** :  

    Mobile Apps ayarlarınızı tıklatın **kolay tabloları** ve tablonuzu seçin. Tıklatın **izinleri değiştirme**seçin **kimlik doğrulamalı erişimi yalnızca** tüm izinleri ve ardından **kaydetmek**.
* **.NET geri bitiş (C#)**:  

    Merhaba sunucu projesinde çok gidin**denetleyicileri** > **TodoItemController.cs**. Merhaba eklemek `[Authorize]` toohello özniteliği **TodoItemController** sınıfı, şu şekilde. toorestrict erişim yalnızca toospecific yöntemleri, bu öznitelik yalnızca toothose yöntemleri hello sınıfı yerine uygulayabilirsiniz. Merhaba sunucu projesi yeniden yayımlayın.

        [Authorize]
        public class TodoItemController : TableController<TodoItem>

* **Node.js arka ucu (üzerinden Node.js kodu)** :  

    Tablo erişimi için toorequire kimlik doğrulamasını satırı toohello Node.js sunucu komut aşağıdaki hello ekleyin:

        table.access = 'authenticated';

    Daha fazla ayrıntı için bkz: [nasıl yapılır: kimlik doğrulaması için erişim tootables gerektiren](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-auth). toodownload hello hızlı başlangıç kod projesinde, sitenizi nasıl görürüm toolearn [nasıl yapılır: indirme hello Node.js arka uç hızlı başlangıç kod projesi Git kullanarak](../articles/app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart).
