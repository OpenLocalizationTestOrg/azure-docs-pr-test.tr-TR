1. Yeni bir pencerede toohello içinde oturum [Azure portal](https://portal.azure.com/).
2. Hello sol bölmede **yeni**, tıklatın **veritabanları**ve ardından **Azure Cosmos DB**, tıklatın **Oluştur**.
   
   ![Hello Azure portal veritabanları bölmesi](./media/cosmos-db-create-dbaccount/create-nosql-db-databases-json-tutorial-1.png)

3. Merhaba üzerinde **yeni hesabı** dikey penceresinde, bu Azure Cosmos DB hesap için istediğiniz hello yapılandırması belirtin. 

    Azure Cosmos DB'de her biri farklı bir hesap gerektiren dört programlama modelinden birini seçebilirsiniz: Gremlin (grafik), MongoDB, SQL (DocumentDB) ve Tablo (anahtar-değer).
    
    Biz program DocumentDB API hello karşı bu hızlı başlangıç makalede, bu nedenle seçin **SQL (DocumentDB)** gibi hello formu doldurun. Bir sosyal medya uygulaması için grafik verileriniz, anahtar/değer (tablo) verileriniz veya bir MongoDB uygulamasından aktarılmış verileriniz varsa Azure Cosmos DB'nin görev açısından kritik tüm uygulamalarınız için yüksek oranda kullanılabilir ve genel olarak dağıtılmış bir veritabanı hizmeti platformu sunacağını unutmayın.

    Tamamlamak hello hello alanları **yeni hesabı** değerlerinizi olarak Kılavuzu - ekran görüntüsü aşağıdaki hello hello bilgileri kullanarak dikey penceresinde hello ekran hello değerleri farklı.
 
    ![Merhaba yeni hesabı dikey penceresinde Azure Cosmos DB](./media/cosmos-db-create-dbaccount/create-nosql-db-databases-json-tutorial-2.png)

    Ayar|Önerilen değer|Açıklama
    ---|---|---
    Kimlik|*Benzersiz değer*|Bu Azure Cosmos DB hesabını tanımlayan benzersiz bir ad. Çünkü *documents.azure.com* eklenmiş toohello kimliği URI, kullanım benzersiz bir ancak tanımlanabilen toocreate sağlamak kimliği olan Merhaba kimliği yalnızca küçük harf, sayı ve hello tire (-) karakterini içerebilir ve 3 too50 karakter içermelidir.
    API|SQL (DocumentDB)|Biz hello karşı program [DocumentDB API](../articles/documentdb/documentdb-introduction.md) bu makalenin ilerisinde yer.|
    Abonelik|*Aboneliğiniz*|Merhaba toouse bu Azure Cosmos DB hesap için istediğiniz Azure aboneliği. 
    Kaynak Grubu|*aynı kimliği olarak değeri hello*|Merhaba yeni kaynak grubu adı, hesabınız için. Kolaylık olması için kimliğinizi hello aynı adı kullanabilirsiniz 
    Konum|*Merhaba bölgeye en yakın tooyour kullanıcılar*|hangi toohost coğrafi konumda Azure Cosmos DB hesabınızı hello. Hızlı erişim toohello veri hello en yakın tooyour kullanıcılar toogive hello konumu seçin.
4. Tıklatın **oluşturma** toocreate hello hesabı.
5. Merhaba Hello üstteki araç çubuğunda tıklatın **bildirimleri** simgesi ![hello bildirim simgesi](./media/cosmos-db-create-dbaccount/notification-icon.png) toomonitor hello dağıtım işlemi.

    ![Hello Azure portal bildirimleri bölmesi](./media/cosmos-db-create-dbaccount-graph/azure-documentdb-nosql-notification.png)

6.  Hello bildirimler penceresini zaman gösterdiği hello dağıtımı başarılı oldu, Kapat hello bildirim penceresi ve açık hello yeni hello hesabından **tüm kaynakları** döşeme hello Pano üzerinde. 

    ![Merhaba tüm kaynakları döşeme hello DocumentDB hesabı](./media/cosmos-db-create-dbaccount/all-resources.png)
 
