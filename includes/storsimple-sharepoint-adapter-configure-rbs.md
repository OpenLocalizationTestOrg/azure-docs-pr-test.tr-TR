<!--author=SharS last changed: 1/14/2016 -->

> [!NOTE]
> SharePoint KKY yapılandırma değişiklikleri toohello StorSimple bağdaştırıcısı yaparken toohello Domain Admins grubuna üye olduğu bir kullanıcı hesabıyla oturum açmanız gerekir. Ayrıca, merkezi yönetim aynı ana bilgisayar hello üzerinde çalışan bir tarayıcıdan hello yapılandırma sayfası erişmeniz gerekir.
> 
> 

#### <a name="tooconfigure-rbs"></a>tooconfigure KKY
1. Merhaba SharePoint Yönetim Merkezi sayfasını açın ve çok gözatın**sistem ayarlarını**. 
2. Merhaba, **Azure StorSimple** 'yi tıklatın **StorSimple bağdaştırıcısı yapılandırma**.
   
    ![Merhaba StorSimple bağdaştırıcısını yapılandırın](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS1-include.png) 
3. Merhaba üzerinde **StorSimple bağdaştırıcısını yapılandırın** sayfa:
   
   1. Bu hello emin olun **düzenleme yolu etkinleştir** onay kutusu seçilidir.
   2. Merhaba metin kutusuna hello BLOB deposu hello Evrensel Adlandırma Kuralı (UNC) yolunu yazın.
      
      > [!NOTE]
      > Merhaba BLOB Depolama Birimi hello StorSimple cihazında yapılandırılmış bir iSCSI birim üzerinde barındırılması gerekir.

   3. Merhaba tıklatın **etkinleştirmek** her bir uzak depolama için tooconfigure istediğiniz hello içerik veritabanı aşağıdaki düğmesine.
      
      > [!NOTE]
      > Merhaba BLOB deposu tüm web ön uç (WFE) sunucuları tarafından paylaşılan ve erişilebilir olması gerekir ve erişim toohello paylaşımı hello SharePoint sunucu grubu için yapılandırılmış hello kullanıcı hesabı olmalıdır.
      
      ![Merhaba KKY sağlayıcısını etkinleştirin](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS2-include.png)
      
      Etkinleştirmek ya da KKY devre dışı iletiden hello ayrıca görürsünüz.
      
      ![StorSimple bağdaştırıcısı etkinleştirme devre dışı bırakma yapılandırın](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_ConfigureStorSimpleAdapterEnableDisableMessage-include.png)

   4. Merhaba tıklatın **güncelleştirme** düğme tooapply hello yapılandırması. Merhaba tıkladığınızda **güncelleştirme** düğmesi tüm WFE sunucularında hello KKY yapılandırma durumu güncelleştirilir ve hello tüm Grup KKY etkin olacaktır. iletiden hello görüntülenir.
      
      ![Bağdaştırıcı yapılandırma iletisi](./media/storsimple-sharepoint-adapter-configure-rbs/HCS_SSASP_ConfigRBS3-include.png)
      
      > [!NOTE]
      > Bir çok sayıda (200'den büyük) veritabanları bir SharePoint çiftliği için KKY yapılandırıyorsanız, zaman aşımı hello SharePoint Yönetim Merkezi web sayfası olabilir. Bu gerçekleşirse, hello sayfayı yenileyin. Bu hello yapılandırma işlemi etkilemez.

4. Merhaba yapılandırmasını doğrulayın:
   
   1. Toohello SharePoint Yönetim Merkezi Web sitesinde oturum ve toohello Gözat **StorSimple bağdaştırıcısını yapılandırın** sayfası.
   2. Merhaba yapılandırma ayrıntıları toomake girdiğiniz hello ayarları eşleştiğinden emin olun. 
5. KKY düzgün çalıştığını doğrulayın:
   
   1. Bir belge tooSharePoint karşıya yükleyin. 
   2. Yapılandırdığınız toohello UNC yoluna göz atın. Merhaba KKY dizin yapısını oluşturulduğunu ve karşıya hello nesne içerir emin olun.
6. (İsteğe bağlı) Merhaba Microsoft RBS kullanabileceğiniz `Migrate()` SharePoint toomigrate mevcut BLOB içerik toohello StorSimple cihazı ile dahil PowerShell cmdlet'i. Daha fazla bilgi için bkz: [içine veya SharePoint 2013'te KKY dışında İçerik Geçişi] [ 6] veya [içine veya dışına KKY (SharePoint Foundation 2010) İçerik Geçişi] [7].
7. (İsteğe bağlı) Test yüklemelerinde hello BLOB'ları gibi hello içerik veritabanı dışında taşındı doğrulayabilirsiniz: 
   
   1. SQL Management Studio'yu başlatın.
   2. Merhaba Listblobsındb_2010.SQL veya Listblobsındb_2013.SQL sorgu aşağıdaki gibi çalıştırın.
      
      ```
      **ListBlobsInDB_2013.sql**
      
        USE WSS_Content
        GO
      
        SELECT DocStreams.DocId,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               DocStreams.RbsId,
               TimeLastModified
      
        FROM DocStreams
      
             INNER JOIN AllDocs ON DocStreams.DocId = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      
      **ListBlobsInDB_2010.sql**
      
        USE WSS_Content
        GO
      
        SELECT AllDocStreams.Id,
      
               LeafName AS Name,
               Content,
               AllDocs.Size AS OrigSizeOfContent,
               LEN(CAST(Content AS VARBINARY(MAX))) AS SizeOfContentInDB,
               RbsId,
               TimeLastModified
        FROM AllDocStreams
      
             INNER JOIN AllDocs ON AllDocStreams.Id = AllDocs.Id
        ORDER BY TimeLastModified DESC
        GO
      ```
      
      KKY doğru şekilde yapılandırıldıysa, bir NULL değer karşıya ve başarıyla KKY ile externalized herhangi bir nesnenin hello SizeOfContentInDB Sütun görüntülenmelidir.
8. (İsteğe bağlı) KKY yapılandırın ve sonra tüm BLOB içerik toohello StorSimple cihazı taşıma hello içerik veritabanını toohello aygıt taşıyabilirsiniz. Toomove hello içerik veritabanını seçerseniz, birincil bir birim olarak hello aygıtta hello içerik veritabanı depolama yapılandırmanızı öneririz. Ardından, kullanım toomigrate hello içerik veritabanını toohello StorSimple cihazı SQL Server en iyi yöntemler kurdu. 
   
   > [!NOTE]
   > Taşıma hello içerik veritabanını toohello cihaz yalnızca hello StorSimple 8000 serisi (bunu hello 5000 veya 7000 Serisi için desteklenmiyor) desteklenir.
   
   Merhaba StorSimple cihazı ayrı birimlerde içinde BLOB'ları ve hello içerik veritabanını depoluyorsanız bunları hello yapılandırmanızı öneririz aynı birim kapsayıcısı. Bu, bunlar birlikte yedeklenecek olmasını sağlar.
   
   > [!WARNING]
   > KKY etkinleştirmediyseniz hello içerik veritabanını toohello StorSimple cihazı taşıma önermiyoruz. Bu sınanmamış bir yapılandırmadır.
   
9. Sonraki adıma gidin toohello: [çöp toplama yapılandırma](#configure-garbage-collection).

[6]: https://technet.microsoft.com/library/ff628254(v=office.15).aspx
[7]: https://technet.microsoft.com/library/ff628255(v=office.14).aspx
