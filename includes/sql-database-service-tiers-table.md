<!--
Used in:
sql-database-performance-guidance.md  
sql-database-resource-limits.md
sql-database-service-tiers.md  
-->

### <a name="basic-service-tier"></a>Temel hizmet katmanı
| **Performans düzeyi** | **Temel** |
| --- | :---: |
| Maks. DTU | 5 |
| Maks. veritabanı boyutu* |2 GB|
| Maks. bellek içi OLTP depolama alanı |Yok |
| En fazla eşzamanlı çalışan (istek sayısı) |30 |
| Maks. eş zamanlı oturum |30 |
| Maks. eş zamanlı oturum |300 |
|||

### <a name="standard-service-tier"></a>Standart hizmet katmanı
| **Performans düzeyi** | **S0** | **S1** | **S2** | **S3** |
| --- |---:| ---:|---:|---:|---:|
| Maks. DTU | 10 | 20 | 50 | 100 |
| Maks. veritabanı boyutu* | 250 GB| 250 GB | 250 GB | 250 GB |
| Maks. bellek içi OLTP depolama alanı | Yok | Yok | Yok | Yok |
| En fazla eşzamanlı çalışan (istek sayısı)| 60 | 90 | 120 | 200 |
| Maks. eş zamanlı oturum | 60 | 90 | 120 | 200 |
| Maks. eş zamanlı oturum |600 | 900 | 1200 | 2400 |
||||||

### <a name="premium-service-tier"></a>Premium hizmet katmanı 
| **Performans düzeyi** | **P1** | **P2** | **P4** | **P6** | **P11** | **P15** | 
| --- |---:|---:|---:|---:|---:|---:|
| Maks. DTU | 125 | 250 | 500 | 1000 | 1750 | 4000 |
| Maks. veritabanı boyutu* | 500 GB | 500 GB | 500  GB | 500 GB | 4 TB | 4 TB |
| Maks. bellek içi OLTP depolama alanı | 1 GB | 2 GB | 4 GB | 8 GB | 14 GB | 32 GB |
| En fazla eşzamanlı çalışan (istek sayısı)| 200 | 400 | 800 | 1600 | 2400 | 6400 |
| Maks. eş zamanlı oturum | 200 | 400| 800| 1600| 2400| 6400 |
| Maks. eş zamanlı oturum | 30000| 30000| 30000| 30000| 30000| 30000 |
|||||||

### <a name="premium-rs-service-tier"></a>Premium RS hizmet katmanı 
| **Performans düzeyi** | **PRS1** | **PRS2** | **PRS4** | **PRS6** |
| --- |---:|---:|---:|---:|---:|---:|
| Maks. DTU | 125 | 250 | 500 | 1000 |
| Maks. veritabanı boyutu* | 500 GB | 500 GB | 500  GB | 500 GB |
| Maks. bellek içi OLTP depolama alanı | 1 GB | 2 GB | 4 GB | 8 GB |
| En fazla eşzamanlı çalışan (istek sayısı)| 200 | 400 | 800 | 1600 |
| Maks. eş zamanlı oturum | 200 | 400| 800| 1600|
| Maks. eş zamanlı oturum | 30000| 30000| 30000| 30000|
|||||||

\* Maksimum veri tabanı boyutu, veritabanındaki verilerin maksimum boyutunu tanımlar. 