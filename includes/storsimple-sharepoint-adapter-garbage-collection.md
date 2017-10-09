<!--author=SharS last changed: 9/17/15-->

Bu yordamda şunları yapacaksınız:

1. [Toorun hello Bakımcı yürütülebilir hazırlama](#to-prepare-to-run-the-maintainer) .
2. [Merhaba içerik veritabanını ve geri dönüşüm kutusu yalnız bırakılmış BLOB'lar anında silme işlemi için hazırlama](#to-prepare-the-content-database-and-recycle-bin-to-immediately-delete-orphaned-blobs).
3. [Maintainer.exe Çalıştır](#to-run-the-maintainer).
4. [Merhaba içerik veritabanı ve geri dönüşüm kutusu ayarlarını geri](#to-revert-the-content-database-and-recycle-bin-settings).

#### <a name="tooprepare-toorun-hello-maintainer"></a>tooprepare toorun hello Bakımcı
1. Merhaba Web ön uç sunucusunda, yönetici olarak hello SharePoint 2013 Yönetim Kabuğu'nu açın.
2. Toohello klasörüne gidin *önyükleme sürücüsü*: \Program SQL Uzak Blob Depolama 10.50\Maintainer\.
3. Yeniden Adlandır **Microsoft.Data.SqlRemoteBlobs.Maintainer.exe.config** çok**web.config**.
4. Kullanım `aspnet_regiis -pdf connectionStrings` toodecrypt hello web.config dosyası.
5. Merhaba altında hello şifresi çözülmüş web.config dosyasında `connectionStrings` düğümü, SQL server örneği için başlangıç bağlantı dizesi eklemek ve hello içerik veritabanı adı. Merhaba aşağıdaki örneğine bakın.
   
    `<add name=”RBSMaintainerConnectionWSSContent” connectionString="Data Source=SHRPT13-SQL12\SHRPT13;Initial Catalog=WSS_Content;Integrated Security=True;Application Name=&quot;Remote Blob Storage Maintainer for WSS_Content&quot;" providerName="System.Data.SqlClient" />`
6. Kullanım `aspnet_regiis –pef connectionStrings` toore-hello web.config dosyasını şifrelemek. 
7. Web.config tooMicrosoft.Data.SqlRemoteBlobs.Maintainer.exe.config yeniden adlandırın. 

#### <a name="tooprepare-hello-content-database-and-recycle-bin-tooimmediately-delete-orphaned-blobs"></a>tooprepare hello içerik veritabanı ve geri dönüşüm kutusu tooimmediately yalnız bırakılmış BLOB'ları silme
1. Merhaba SQL Management Studio'da, SQL Server üzerinde güncelleştirme sorguları hello hedef içerik veritabanı için aşağıdaki hello çalıştırın: 
   
       `use WSS_Content`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ’time 00:00:00’`
   
       `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’time 00:00:00’`
2. Merhaba üzerinde web ön uç sunucusu altında **Merkezi Yönetim**, hello Düzenle **Web uygulaması genel ayarları** hello istenen içerik veritabanını tootemporarily devre dışı bırak hello geri dönüşüm kutusu için. Bu eylem boş hello geri dönüşüm kutusu tüm ilgili site koleksiyonları için de olur. toodo bunu, **Merkezi Yönetim** -> **Uygulama Yönetimi** -> **Web uygulamaları (web uygulamalarını yönet)**  ->  **SharePoint - 80** -> **genel uygulama ayarları**. Set hello **Geri Dönüşüm Kutusu'nu durumu** çok**OFF**.
   
    ![Web uygulaması genel ayarları](./media/storsimple-sharepoint-adapter-garbage-collection/HCS_WebApplicationGeneralSettings-include.png)

#### <a name="toorun-hello-maintainer"></a>toorun hello Bakımcı
* Merhaba web ön uç sunucusunda, hello SharePoint 2013 Yönetim Kabuğu hello Bakımcı aşağıdaki gibi çalıştırın:
  
      `Microsoft.Data.SqlRemoteBlobs.Maintainer.exe -ConnectionStringName RBSMaintainerConnectionWSSContent -Operation GarbageCollection -GarbageCollectionPhases rdo`
  
  > [!NOTE]
  > Yalnızca hello `GarbageCollection` işlemi şu anda StorSimple için desteklenir. Ayrıca Microsoft.Data.SqlRemoteBlobs.Maintainer.exe için verilen hello parametreleri büyük küçük harfe duyarlı olduğunu unutmayın. 
  > 
  > 

#### <a name="toorevert-hello-content-database-and-recycle-bin-settings"></a>toorevert hello içerik veritabanını ve Geri Dönüşüm Kutusu ayarları
1. Merhaba SQL Management Studio'da, SQL Server üzerinde güncelleştirme sorguları hello hedef içerik veritabanı için aşağıdaki hello çalıştırın:
   
      `use WSS_Content`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘garbage_collection_time_window’ , ‘days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘delete_scan_period’ , ’days 30’`
   
      `exec mssqlrbs.rbs_sp_set_config_value ‘orphan_scan_period’ , ’days 30’`
2. Ön uç web sunucusuna Merhaba, içinde **Merkezi Yönetim**, hello Düzenle **Web uygulaması genel ayarları** hello istenen içerik veritabanını toore etkinleştir hello geri dönüşüm kutusu için. toodo bunu, **Merkezi Yönetim** -> **Uygulama Yönetimi** -> **Web uygulamaları (web uygulamalarını yönet)**  ->  **SharePoint - 80** -> **genel uygulama ayarları**. Merhaba Geri Dönüşüm Kutusu'nu durumu çok ayarlamak**ON**.

