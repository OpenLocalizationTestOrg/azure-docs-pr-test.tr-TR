<!--author=alkohli last changed:02/10/2017-->


#### <a name="toocreate-a-new-service"></a>toocreate yeni bir hizmet

1. Microsoft hesabı kimlik bilgileri toolog üzerinde toohello kullanmak [Azure portal](https://portal.azure.com/).

2. Hello Azure portal'ı tıklatın  **+**  ve hello marketi'ndeki ardından **tümünü görmek**.

    ![StorSimple Cihaz Yöneticisi oluşturma](./media/storsimple-8000-create-new-service/createssdevman1.png)

    _StorSimple Fiziksel_ ifadesini aratın. **StorSimple Fiziksel Cihaz Serisi**‘ni seçip tıklayın ve **Oluştur**’a tıklayın. Alternatif olarak, hello Azure portal'ı tıklatın  **+**  altında ve **depolama**, tıklatın **StorSimple fiziksel cihazı seri**.

    ![StorSimple Cihaz Yöneticisi oluşturma](./media/storsimple-8000-create-new-service/createssdevman11.png)

3. Merhaba, **StorSimple Aygıt Yöneticisi'ni** dikey penceresinde, adımları hello:
   
   1. Hizmetiniz için benzersiz bir **Kaynak adı** sağlayın. Bu ad olabilecek bir kolay addır tooidentify hello hizmeti kullanılır. Merhaba adı harf, rakam ve kısa çizgi olabilir 2 ile 50 karakter uzunluğunda olabilir. Merhaba adı başlamalı ve bir harf veya sayı ile bitmelidir.

   2. Seçin bir **abonelik** hello aşağı açılan listeden. Merhaba abonelik hesabı faturalama bağlantılı tooyour ' dir. Bu alan bir aboneliğiniz olmadığı sürece yoktur.

   3. **Kaynak Grubu** için **Mevcut grubu kullanın** veya **Yeni grup oluşturun**. Daha fazla bilgi edinmek için bkz. [Azure kaynak grupları](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-infrastructure-resource-groups-guidelines/).
   
   4. Hizmetiniz için bir **Konum** sağlayın. Genel olarak, Cihazınızı toodeploy istediğiniz konum en yakın toohello coğrafi bölge seçin. Ayrıca, ilgili önemli noktalar aşağıdaki hello toofactor isteyebilirsiniz: 
      
      * Var olan iş yükleri toodeploy de StorSimple cihazınızla düşündüğünüz Azure varsa, o veri merkezini kullanmanız gerekir.
      * StorSimple Cihaz Yöneticisi hizmeti ve Azure Storage iki ayrı konumda olabilir. Böyle bir durumda, gerekli toocreate hello StorSimple Aygıt Yöneticisi'ni ve Azure depolama hesabı ayrı olarak demektir. toocreate bir Azure depolama hesabı toohello Azure depolama hizmetinde hello Azure portalına gidin ve'hello adımlarını izleyin [bir Azure depolama hesabı oluşturma](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account). Bu hesabı oluşturduktan sonra hello adımları izleyerek toohello StorSimple cihaz Yöneticisi hizmeti eklemek [hello hizmet için yeni bir depolama hesabı yapılandırma](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#configure-a-new-storage-account-for-the-service).

   5. Seçin **yeni depolama hesabı oluşturma** tooautomatically hello hizmeti ile bir depolama hesabı oluşturun. Bu depolama hesabı için bir ad belirtin. Verilerinizin farklı bir konumda olması gerekiyorsa bu kutunun işaretini kaldırın.

   6. Denetleme **PIN toodashboard** hızlı bağlantıyı toothis hizmeti Panonuzda istiyorsanız.
      
   7. Tıklatın **oluşturma** toocreate hello StorSimple cihaz Yöneticisi.

       ![StorSimple Cihaz Yöneticisi oluşturma](./media/storsimple-8000-create-new-service/createssdevman2.png)
   
Merhaba hizmeti oluşturulması birkaç dakika sürer. Merhaba hizmeti başarıyla oluşturulduktan sonra bir bildirim görürsünüz ve hello yeni hizmet dikey penceresi açılır.
   
![StorSimple Cihaz Yöneticisi oluşturma](./media/storsimple-8000-create-new-service/createssdevman5.png)


