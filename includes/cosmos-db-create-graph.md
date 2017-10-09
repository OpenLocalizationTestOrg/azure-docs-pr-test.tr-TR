Artık hello Azure portal toocreate bir grafik veritabanı hello Veri Gezgini aracını kullanabilirsiniz. 

1. Merhaba hello sol gezinti menüsünde, Azure portal'ı tıklatın **Veri Gezgini (Önizleme)**. 
2. Merhaba, **Veri Gezgini (Önizleme)** dikey penceresinde tıklatın **yeni bir grafik**, aşağıdaki bilgilerle hello kullanarak hello sayfasında doldurun.

    ![Hello Azure portal'ın Veri Gezgini](./media/cosmos-db-create-graph/azure-cosmosdb-data-explorer.png)

    Ayar|Önerilen değer|Açıklama
    ---|---|---
    Veritabanı kimliği|sample-database|Yeni veritabanı Hello kimliği. Veritabanı adı 1 ile 255 karakter arasında olmalı, `/ \ # ?` içermemeli ve boşlukla bitmemelidir.
    Grafik kimliği|sample-graph|Merhaba kimliği, yeni bir grafik. Grafik adlara sahip hello veritabanı kimlikleri aynı karakter gereksinimleri.
    Depolama Kapasitesi| 10 GB|Merhaba varsayılan değeri bırakın. Merhaba depolama kapasitesi hello veritabanının budur.
    Aktarım hızı|400 RU|Merhaba varsayılan değeri bırakın. Tooreduce gecikme istiyorsanız hello verimlilik daha sonra ölçeklendirebilirsiniz.
    Bölüm anahtarı|/userid|Veri eşit olarak dağıtmanızı bir bölüm anahtarı tooeach bölüm. Grafik Hello bölüm anahtarı bir kullanıcı oluşturmak önemlidir doğru seçerek, içinde hakkında daha fazla bilgi [bölümleme için tasarlama](../articles/cosmos-db/partition-data.md#designing-for-partitioning).

3. Merhaba form doldurulur sonra tıklayın **Tamam**.
