Artık hello Veri Gezgini aracında hello Azure portal toocreate bir veritabanı ve koleksiyonu da kullanabilirsiniz. 

1. Merhaba hello sol gezinti menüsünde, Azure portal'ı tıklatın **Veri Gezgini (Önizleme)**. 

2. Merhaba üzerinde **Veri Gezgini (Önizleme)** dikey penceresinde tıklatın **yeni koleksiyon**ve ardından aşağıdaki bilgilerle hello sağlayın:

    ![Hello Azure portal Veri Gezgini dikey penceresi](./media/cosmos-db-create-collection/azure-cosmosdb-data-explorer.png)

    Ayar|Önerilen değer|Açıklama
    ---|---|---
    Veritabanı kimliği|Görevler|Yeni veritabanı Hello adı. Veritabanı adı 1 ila 255 karakterden oluşmalı, boşlukla bitmemeli ve şu karakterleri içermemelidir: /, \\, # ve ?.
    Koleksiyon kimliği|Öğeler|Yeni koleksiyonunuzu Hello adı. Koleksiyon adlara sahip hello kimlikleri veritabanı gereksinimleri aynı karakter.
    Depolama kapasitesi| Sabit (10 GB)|Merhaba varsayılan değeri kullanın. Bu değer hello depolama kapasitesi hello veritabanının olur.
    Aktarım hızı|400 RU|Merhaba varsayılan değeri kullanın. Tooreduce gecikme istiyorsanız, daha sonra hello verimlilik ölçeklendirebilirsiniz.
    Bölüm anahtarı|/kategori|Veri dağıtır bir bölüm anahtarı tooeach bölüm. Seçme hello doğru bölüm anahtarı, bir kullanıcı koleksiyonu oluşturma önemlidir. toolearn daha, fazla [bölümleme için tasarlama](../articles/cosmos-db/partition-data.md#designing-for-partitioning).    
3. Merhaba formunu tamamladıktan sonra tıklatın **Tamam**.

Veri Gezgini'ni gösterir, yeni veritabanı ve koleksiyonu hello. 
