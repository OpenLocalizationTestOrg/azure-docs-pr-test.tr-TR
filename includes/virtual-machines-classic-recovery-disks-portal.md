Azure, sanal makine (VM) önyükleme veya disk bir hatayla karşılaştığında, sorun giderme adımları hello sanal sabit diske kendisini tooperform gerekebilir. Yaygın bir örnek hello VM başarılı bir şekilde önyüklenmesini engeller başarısız uygulama güncelleştirmesi olacaktır. Bu makalede nasıl toouse Azure portal tooconnect, sanal sabit disk tooanother VM toofix hataları ve özgün VM'yi yeniden oluşturun.

## <a name="recovery-process-overview"></a>Kurtarma işlemine genel bakış
sorun giderme işlemi hello aşağıdaki gibidir:

1. Merhaba sorunları karşılaşıyor VM silme ancak hello sanal sabit diskleri korunur.
2. Ekleme ve sorun giderme için hello sanal sabit disk tooanother VM bağlayın.
3. VM sorun giderme toohello bağlayın. Dosyaları düzenleyin veya Araçlar toofix hataları hello özgün sanal sabit disk üzerinde çalıştırın.
4. Çıkarın ve VM sorun giderme hello hello sanal sabit diski kullanımdan çıkarın.
5. Merhaba özgün sanal sabit disk kullanarak bir VM oluşturun.

## <a name="delete-hello-original-vm"></a>Silme özgün VM hello
Sanal sabit diskler ve sanal makineler Azure'da iki ayrı kaynaktır. Bir sanal sabit disk hello işletim sistemi, uygulamalar ve yapılandırmalar depolandığı ' dir. Merhaba VM hello boyutunu veya konumunu tanımlar ve bir sanal sabit disk veya sanal ağ arabirim kartı (NIC) gibi kaynakları başvuran meta verilerdir. Her sanal sabit disk, disk ekli tooa VM olduğunda atanmış bir kira alır. Veri diskleri bağlı ve hatta hello VM çalışırken ayrılmış olsa da, hello VM kaynak silinmedikçe hello işletim sistemi diski ayrılamıyor. Bu VM durduruldu ve deallocated durumda olduğunda bile hello kira tooassociate hello işletim sistemi disk tooa VM devam eder.

İlk adım toorecovering hello VM toodelete hello VM kendisini kaynaktır. Silme hello VM hello sanal sabit diskleri depolama hesabınızdaki bırakır. VM silinmiş hello sonra hello sanal sabit disk tooanother VM tootroubleshoot ekleyin ve hello hataları giderin. 

1. İçinde toohello oturum [Azure portal](https://portal.azure.com). 
2. Merhaba hello sol tarafında menüsünde **sanal makineleri (Klasik)**.
3. Select hello hello sorunlu VM tıklatın **diskleri**ve hello sanal sabit disk hello adını belirleyin. 
4. Merhaba Hello işletim sistemi sanal sabit disk seçin ve **konumu** sanal sabit disk içeren tooidentify hello depolama hesabı. Aşağıdaki örneğine hello dize hemen önce hello ". blob.core.windows.net" Merhaba depolama hesap adı.

    ```
    https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd
    ```

    ![Merhaba görüntü VM'in konumu hakkında](./media/virtual-machines-classic-recovery-disks-portal/vm-location.png)

5. Merhaba VM sağ tıklayın ve ardından **silmek**. Merhaba diskleri hello VM sildiğinizde seçili olmadığından emin olun.
6. Yeni bir kurtarma VM’si oluşturun. Bu VM hello olmalıdır aynı bölge ve kaynak grubu (bulut hizmeti) hello sorun VM.
7. Merhaba kurtarma VM seçin ve ardından **diskleri** > **Attach varolan**.
8. tooselect, mevcut sanal sabit diski tıklatın **VHD dosyasını**:

    ![Mevcut bir VHD'ye göz atma](./media/virtual-machines-classic-recovery-disks-portal/select-vhd-location.png)

9. Hello depolama hesabını seçin > VHD kapsayıcı > sanal sabit disk Merhaba, hello tıklatın **seçin** tooconfirm tercih ettiğiniz düğmesi.

    ![Mevcut VHD’nizi seçme](./media/virtual-machines-classic-recovery-disks-portal/select-vhd.png)

10. Artık seçili, VHD ile seçin **Tamam** tooattach hello varolan bir sanal sabit diski.
11. Birkaç saniye sonra hello **diskleri** bölmesinde, sanal makine için varolan bir sanal sabit bir veri diski bağlı disk görüntülenir:

    ![Veri diski olarak bağlı olan sanal sabit disk](./media/virtual-machines-classic-recovery-disks-portal/attached-disk.png)

## <a name="fix-issues-on-hello-original-virtual-hard-disk"></a>Merhaba özgün sanal sabit disk üzerinde ilgili sorunları giderme
Merhaba varolan bir sanal sabit diski bağlandığında, artık tüm bakım ve sorun giderme adımları gereken şekilde gerçekleştirebilirsiniz. Merhaba sorunlar ele sonra aşağıdaki adımları hello ile devam edin.

## <a name="unmount-and-detach-hello-original-virtual-hard-disk"></a>Çıkarın ve hello özgün sanal sabit disk ayırma
Hataları çözümlendiği sonra çıkarın ve hello varolan sanal sabit diskten, sorun giderme VM ayırma. VM sorun giderme hello sanal sabit disk toohello iliştirir hello kira serbest kadar sanal sabit diski başka bir VM ile birlikte kullanamazsınız.  

1. İçinde toohello oturum [Azure portal](https://portal.azure.com). 
2. Merhaba sol tarafında Hello menüsünde seçin **sanal makineleri (Klasik)**.
3. Merhaba kurtarma VM bulun. Diskler, sağ hello disk seçin ve ardından **ayırma**.

## <a name="create-a-vm-from-hello-original-hard-disk"></a>Merhaba özgün sabit diskten bir VM oluşturma

bir VM, özgün sanal sabit diskten toocreate kullanmak [Klasik Azure portalı](https://manage.windowsazure.com).

1. [Klasik Azure Portalı](https://manage.windowsazure.com)’nda oturum açın.
2. Merhaba portal Hello altındaki seçin **yeni** > **işlem** > **sanal makine** > **Galeri'den** .
3. Merhaba, **bir görüntü seçin** bölümünde, select **disklerim**, ve ardından özgün sanal sabit disk seçin hello. Merhaba konum bilgilerine bakın. Bu hello VM dağıtıldığı gerekir hello bölgedir. Merhaba İleri düğmesini seçin.
4. Merhaba, **sanal makine yapılandırması** bölümünde hello VM adını yazın ve hello VM boyutunu seçin.
