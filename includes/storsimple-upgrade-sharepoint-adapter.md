<!--author=SharS last changed: 9/17/15-->

### <a name="upgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-storsomple-adapter-for-sharepoint"></a>SharePoint 2010 tooSharePoint 2013 yükseltin ve sonra SharePoint için hello StorSomple bağdaştırıcısı yükleyin
> [!IMPORTANT]
> Tüm daha önce KKY aracılığıyla tooexternal depolamaya hello yükseltme işlemi tamamlanana kadar kullanılamaz taşınan dosyaları ve hello KKY özelliği yeniden etkinleştirildi. toolimit kullanıcı etkisi, herhangi bir yükseltme veya planlı bakım penceresi sırasında yeniden gerçekleştirin.
> 
> 

#### <a name="tooupgrade-sharepoint-2010-toosharepoint-2013-and-then-install-hello-adapter"></a>SharePoint 2010 tooupgrade tooSharePoint 2013 ve ardından yükleme hello bağdaştırıcısı
1. SharePoint 2010 Hello grupta hello BLOB Depolama hello yolunu not BLOB'ları ve hello içerik veritabanları KKY etkin olduğu externalized. 
2. Yükleyin ve hello yeni SharePoint 2013 grubuna yapılandırın. 
3. Veritabanları, uygulamaları ve site koleksiyonları hello SharePoint 2010 Grup toohello yeni SharePoint 2013 grubundan taşıyın. Yönergeler için çok gidin[hello yükseltme işlemi tooSharePoint 2013 genel bakış](https://technet.microsoft.com/library/cc262483.aspx).
4. Merhaba yeni gruptaki SharePoint için StorSimple bağdaştırıcısı Hello yükleyin. Çok Git[yükleme hello SharePoint için StorSimple bağdaştırıcısı](#install-the-storsimple-adapter-for-sharepoint) yordamlar.
5. 1. adımda not ettiğiniz hello bilgileri kullanarak, aynı içerik veritabanları ayarlayın ve aynı BLOB hello SharePoint 2010 yüklemesinde kullanılan yolu depolamak hello sağlamak hello için KKY etkinleştirin. Çok Git[yapılandırma KKY](#configure-rbs) yordamlar. Bu adımı tamamladıktan sonra daha önce externalized dosyaları hello yeni grubundan erişilebilir olması gerekir. 

### <a name="upgrade-hello-storsimple-adapter-for-sharepoint"></a>Yükseltme hello SharePoint için StorSimple bağdaştırıcısı
> [!IMPORTANT]
> Aşağıdaki nedenlerden hello için planlı bakım penceresi sırasında bu yükseltme toooccur zamanlamanız gerekir:
> 
> * Daha önce externalized içerik Hello bağdaştırıcısı yeniden kadar kullanılamaz.
> * SharePoint için StorSimple bağdaştırıcısı hello hello önceki sürümünü kaldırın, ancak hello yeni sürümü yüklemeden önce hello içerik veritabanında depolanan sonra herhangi bir içerik toohello site karşıya yüklendi. Merhaba yeni bağdaştırıcısı yükledikten sonra içerik toohello StorSimple cihazı toomove gerekir. Merhaba Microsoft kullanabilirsiniz` RBS Migrate()` SharePoint toomigrate Merhaba içeriğine dahil PowerShell cmdlet'i. Daha fazla bilgi için bkz: [içine veya dışına KKY İçerik Geçişi](https://technet.microsoft.com/library/ff628255.aspx). 
> 
> 

#### <a name="tooupgrade-hello-storsimple-adapter-for-sharepoint"></a>tooupgrade hello SharePoint için StorSimple bağdaştırıcısı
1. SharePoint için StorSimple bağdaştırıcısı Hello önceki sürümünü kaldırın.
   
   > [!NOTE]
   > Bu otomatik olarak KKY hello içerik veritabanlarında devre dışı bırakır. Ancak, mevcut BLOB'ları hello StorSimple aygıtta kalır. KKY devre dışı bırakılır ve hello BLOB'lar geçirilen geri toohello içerik veritabanları edilmemiş, bu BLOB'lar için tüm istekler başarısız olur. 
   > 
   > 
2. SharePoint için yeni StorSimple bağdaştırıcısı hello yükleyin. Merhaba yeni bağdaştırıcısı önceden etkinleştirilmiş veya devre dışı KKY için hello içerik veritabanları otomatik olarak algılar ve hello önceki ayarları kullanır.

