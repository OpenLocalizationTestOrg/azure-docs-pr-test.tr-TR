<!--
Used in:
sql-database-elastic-pool.md   
sql-database-resource-limits.md
sql-database-service-tiers.md  
-->
 
### <a name="basic-elastic-pool-limits"></a>Temel esnek havuz sınırları

| Havuz boyutu (eDTU)  | **50** | **100** | **200** | **300** | **400** | **800** | **1200** | **1600** |
|:---|---:|---:|---:| ---: | ---: | ---: | ---: | ---: |
| Havuz başına maks. veri depolama alanı* | 5 GB | 10 GB | 20 GB | 29 GB | 39 GB | 78 GB | 117 GB | 156 GB |
| Havuz başına maks. Bellek İçi OLTP depolama alanı | Yok | Yok | Yok | Yok | Yok | Yok | Yok | Yok |
| Havuz başına en fazla veritabanı | 100 | 200 | 500 | 500 | 500 | 500 | 500 | 500 |
| Havuz başına maks. eş zamanlı çalışan (istek) | 100 | 200 | 400 | 600 | 800 | 1600 | 2400 | 3200 |
| Havuz başına maks. eş zamanlı oturum | 100 | 200 | 400 | 600 | 800 | 1600 | 2400 | 3200 |
| Havuz başına maks. eş zamanlı oturum | 30000 | 30000 | 30000 | 30000 |30000 | 30000 | 30000 | 30000 |
| Veritabanı başına Min. eDTU | 0, 5 | 0, 5 | 0, 5 | 0, 5 | 0, 5 | 0, 5 | 0, 5 | 0, 5 |
| Veritabanı başına Maks. eDTU | 5 | 5 | 5 | 5 | 5 | 5 | 5 | 5 |
| Veritabanı başına maks. veri depolama alanı | 2 GB | 2 GB | 2 GB | 2 GB | 2 GB | 2 GB | 2 GB | 2 GB | 
||||||||

### <a name="standard-elastic-pool-limits"></a>Standart esnek havuz sınırları

| Havuz boyutu (eDTU)  | **50** | **100** | **200**** | **300**** | **400**** | **800****| 
|:---|---:|---:|---:| ---: | ---: | ---: | 
| Havuz başına maks. veri depolama alanı* | 50 GB| 100 GB| 200 GB | 300 GB| 400 GB | 800 GB | 
| Havuz başına maks. Bellek İçi OLTP depolama alanı | Yok | Yok | Yok | Yok | Yok | Yok | 
| Havuz başına en fazla veritabanı | 100 | 200 | 500 | 500 | 500 | 500 | 
| Havuz başına maks. eş zamanlı çalışan (istek) | 100 | 200 | 400 | 600 |  800 | 1600 |
| Havuz başına maks. eş zamanlı oturum | 100 | 200 | 400 | 600 |  800 | 1600 |
| Havuz başına maks. eş zamanlı oturum | 30000 | 30000 | 30000 | 30000 | 30000 | 30000 |
| Veritabanı başına Min. eDTU** | 0, 10, 20, 50 | 0, 10, 20, 50, 100 | 0, 10, 20, 50, 100, 200 | 0, 10, 20, 50, 100, 200, 300 | 0, 10, 20, 50, 100, 200, 300, 400 | 0, 10, 20, 50, 100, 200, 300, 400, 800 |
| Veritabanı başına Maks. eDTU** | 10, 20, 50 | 10, 20, 50, 100 | 10, 20, 50, 100, 200 | 10, 20, 50, 100, 200, 300 | 10, 20, 50, 100, 200, 300, 400 | 10, 20, 50, 100, 200, 300, 400, 800 | 
| Veritabanı başına maks. veri depolama alanı | 50 GB | 100 GB | 200 GB | 250 GB | 250 GB | 250 GB |
||||||||

### <a name="standard-elastic-pool-limits-continued"></a>Standart esnek havuz limitleri (devam) 

| Havuz boyutu (eDTU)  |  **1200**** | **1600**** | **2000**** | **2500**** | **3000**** |
|:---|---:|---:|---:| ---: | ---: |
| Havuz başına maks. veri depolama alanı* | 1,2 TB | 1,6 TB | 2 TB | 2,4 TB | 2,9 TB | 
| Havuz başına maks. Bellek İçi OLTP depolama alanı | Yok | Yok | Yok | Yok | Yok | 
| Havuz başına en fazla veritabanı | 500 | 500 | 500 | 500 | 500 | 
| Havuz başına maks. eş zamanlı çalışan (istek) |  2400 | 3200 | 4000 | 5000 | 6000 |
| Havuz başına maks. eş zamanlı oturum |  2400 | 3200 | 4000 | 5000 | 6000 |
| Havuz başına maks. eş zamanlı oturum | 30000 | 30000 | 30000 | 30000 | 30000 | 
| Veritabanı başına Min. eDTU** | 0, 10, 20, 50, 100, 200, 300, 400, 800, 1200 | 0, 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600 | 0, 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600, 2000 | 0, 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600, 2000, 2500 | 0, 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600, 2000, 2500, 3000 |
| Veritabanı başına Maks. eDTU** | 10, 20, 50, 100, 200, 300, 400, 800, 1200 | 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600 | 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600, 2000 | 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600, 2000, 2500 | 10, 20, 50, 100, 200, 300, 400, 800, 1200, 1600, 2000, 2500, 3000 | 
| Veritabanı başına maks. veri depolama alanı | 250 GB | 250 GB | 250 GB | 250 GB | 250 GB | 
||||||||

### <a name="premium-elastic-pool-limits"></a>Premium esnek havuz sınırları

| Havuz boyutu (eDTU)  | **125** | **250** | **500** | **1000** | **1500*****| 
|:---|---:|---:|---:| ---: | ---: | 
| Havuz başına maks. veri depolama alanı* | 250 GB | 500 GB | 750 GB | 1 TB | 1,5 TB | 
| Havuz başına maks. Bellek İçi OLTP depolama alanı | 1 GB| 2 GB| 4 GB| 10 GB| 12 GB| 
| Havuz başına en fazla veritabanı | 50 | 100 | 100 | 100 | 100 |  
| Havuz başına maks. eş zamanlı çalışan (istek) | 200 | 400 | 800 | 1600 |  2400 | 
| Havuz başına maks. eş zamanlı oturum | 200 | 400 | 800 | 1600 |  2400 |
| Havuz başına maks. eş zamanlı oturum | 30000 | 30000 | 30000 | 30000 | 30000 | 
| Veritabanı başına Min. eDTU | 0, 25, 50, 75, 125 | 0, 25, 50, 75, 125, 250 | 0, 25, 50, 75, 125, 250, 500 | 0, 25, 50, 75, 125, 250, 500, 1000 | 0, 25, 50, 75, 125, 250, 500, 1000 | 
| Veritabanı başına Maks. eDTU | 25, 50, 75, 125 | 25, 50, 75, 125, 250 | 25, 50, 75, 125, 250, 500 | 25, 50, 75, 125, 250, 500, 1000 | 25, 50, 75, 125, 250, 500, 1000 |
| Veritabanı başına maks. veri depolama alanı | 250 GB | 500 GB | 500 GB | 500 GB | 500 GB | 
||||||||

### <a name="premium-elastic-pool-limits-continued"></a>Premium esnek havuz limitleri (devam) 

| Havuz boyutu (eDTU) | **2000***** | **2500***** | **3000***** | **3500***** | **4000*****|
|:---|---:|---:|---:| ---: | ---: | 
| Havuz başına maks. veri depolama alanı* | 2 TB | 2,5 TB | 3 TB | 3,5 TB | 4 TB |
| Havuz başına maks. Bellek İçi OLTP depolama alanı | 16 GB | 20 GB | 24 GB | 28 GB | 32 GB |
| Havuz başına en fazla veritabanı | 100 | 100 | 100 | 100 | 100 | 
| Havuz başına maks. eş zamanlı çalışan (istek) |  3200 | 4000 | 4800 | 5600 | 6400 |
| Havuz başına maks. eş zamanlı oturum |  3200 | 4000 | 4800 | 5600 | 6400 |
| Havuz başına maks. eş zamanlı oturum | 30000 | 30000 | 30000 | 30000 | 30000 | 
| Veritabanı başına Min. eDTU | 0, 25, 50, 75, 125, 250, 500, 1000, 1750 | 0, 25, 50, 75, 125, 250, 500, 1000, 1750 | 0, 25, 50, 75, 125, 250, 500, 1000, 1750 | 0, 25, 50, 75, 125, 250, 500, 1000, 1750 |  0, 25, 50, 75, 125, 250, 500, 1000, 1750, 4000 | 
| Veritabanı başına Maks. eDTU | 25, 50, 75, 125, 250, 500, 1000, 1750 | 25, 50, 75, 125, 250, 500, 1000, 1750 | 25, 50, 75, 125, 250, 500, 1000, 1750 | 25, 50, 75, 125, 250, 500, 1000, 1750 | 25, 50, 75, 125, 250, 500, 1000, 1750, 4000 | 
| Veritabanı başına maks. veri depolama alanı | 500 GB | 500 GB | 500 GB | 500 GB | 500 GB | 
||||||||

### <a name="premium-rs-elastic-pool-limits"></a>Premium RS elastik havuz sınırları

| Havuz boyutu (eDTU)  | **125** | **250** | **500** | **1000** |
|:---|---:|---:|---:| ---: | ---: | 
| Havuz başına maks. veri depolama alanı* | 250 GB| 500 GB | 750 GB | 750 GB |
| Havuz başına maks. Bellek İçi OLTP depolama alanı | 1 GB | 2 GB | 4 GB | 10 GB |
| Havuz başına en fazla veritabanı | 50 | 100 | 100 | 100 |
| Havuz başına maks. eş zamanlı çalışan (istek) | 200 | 400 | 800 | 1600 |
| Havuz başına maks. eş zamanlı oturum | 200 | 400 | 800 | 1600 |
| Havuz başına maks. eş zamanlı oturum | 30000 | 30000 | 30000 | 30000 |
| Veritabanı başına Min. eDTU | 0, 25, 50, 75, 125 | 0, 25, 50, 75, 125, 250 | 0, 25, 50, 75, 125, 250, 500 | 0, 25, 50, 75, 125, 250, 500, 1000 |
| Veritabanı başına Maks. eDTU | 25, 50, 75, 125 | 25, 50, 75, 125, 250 | 25, 50, 75, 125, 250, 500 | 25, 50, 75, 125, 250, 500, 1000 | 
| Veritabanı başına maks. veri depolama alanı | 250 GB | 500 GB | 500 GB | 500 GB | 
||||||||

> [!IMPORTANT]
>\*Esnek havuzdaki veri depolama sınırlı toohello hello kalan havuz depolama veya veritabanı başına en fazla depolama daha küçük olacak şekilde havuza alınmış veritabanları havuzu depolama paylaşır. 
>
>
>\*\* Veritabanı başına 200 eDTU ve üzerinden başlayan min/maks eDTU genel önizleme aşamasındadır.
>
>\*\*\*Premium havuzlarıyla 500 Edtu havuzu başına Hello varsayılan en büyük veri depolama veya daha fazla 750 GB'dir. tooobtain Merhaba 1000 veya daha fazla Edtu'lar için Premium havuz başına daha yüksek bir maksimum veri depolama boyutu, bu boyut hello Azure portal kullanarak açıkça seçilmelidir [PowerShell](../articles/sql-database/sql-database-elastic-pool.md#manage-sql-database-elastic-pools-using-powershell), hello [Azure CLI](../articles/sql-database/sql-database-elastic-pool.md#manage-sql-database-elastic-pools-using-the-azure-cli), veya hello [REST API](../articles/sql-database/sql-database-elastic-pool.md#manage-sql-database-elastic-pools-using-the-rest-api). Premium fazla 1 TB depolama havuzlarıyla olan şu anda bölgeleri aşağıdaki hello genel önizlemede: BİZE East2, Batı ABD, BİZE kamu Virginia, Batı Avrupa, Orta Almanya, Güney Doğu Asya, Japonya Doğu, Avustralya Doğu, Kanada merkezi ve Doğu Kanada. diğer tüm bölgeler için havuz başına en fazla depolama Hello şu anda sınırlı too750 GB'dir.
>
