Azure’da artık iki hata ayıklama özelliği desteklenmektedir: Azure Sanal Makineler Kaynak Yöneticisi dağıtım modelinde Konsol Çıktısı ve Ekran Görüntüsü desteği vardır. 

Kendi görüntü tooAzure veya hello platform görüntüleri bile önyükleme biri getirilirken bir sanal makine önyüklenebilir olmayan bir duruma neden alır birçok nedeni olabilir. Bu özellikler, tooeasily tanılamak ve sanal makinelerinizi önyükleme hatalarını kurtarıp etkinleştir.

Linux sanal makineleri için hello Portal, konsol günlüğünden hello çıktısını kolayca görüntüleyebilirsiniz:

![Azure portalına](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
Ancak, Windows ve Linux sanal makineleri için Azure ayrıca bir ekran görüntüsünü hello VM hello hiper yönetici gelen toosee sağlar:

![Hata](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

Bu özelliklerin her ikisi de tüm bölgelerdeki Azure sanal makineler için desteklenir. Not, ekran görüntüleri ve çıktı too10 dakika tooappear depolama hesabınızdaki yukarı alabilir.

## <a name="common-boot-errors"></a>Sık karşılaşılan önyükleme hataları

- [0xC000000E](https://support.microsoft.com/help/4010129)
- [0xC000000F](https://support.microsoft.com/help/4010130)
- [0xC0000011](https://support.microsoft.com/help/4010134)
- [0xC0000034](https://support.microsoft.com/help/4010140)
- [0xC0000098](https://support.microsoft.com/help/4010137)
- [0xC00000BA](https://support.microsoft.com/help/4010136)
- [0xC000014C](https://support.microsoft.com/help/4010141)
- [0xC0000221](https://support.microsoft.com/help/4010132)
- [0xC0000225](https://support.microsoft.com/help/4010138)
- [0xC0000359](https://support.microsoft.com/help/4010135)
- [0xC0000605](https://support.microsoft.com/help/4010131)
- [Bir işletim sistemi bulunamadı](https://support.microsoft.com/help/4010142)
- [Önyükleme hatası veya INACCESSIBLE_BOOT_DEVICE](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Yeni bir sanal makine üzerinde tanılamayı etkinleştir
1. Önizleme portalı hello yeni bir sanal makine oluştururken, hello seçin **Azure Resource Manager** gelen hello dağıtım modeli açılır:
 
    ![Resource Manager](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. Bu tanılama dosyaları Hello tooplace oluşturulacağı yeri izleme seçeneği tooselect hello depolama hesabı yapılandırın.
 
    ![VM oluşturma](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. Bir Azure Resource Manager şablonu dağıtıyorsanız, tooyour sanal makine kaynağı gidin ve hello tanılama profil bölümü ekleyin. Toouse hello "2015-06-15" API sürümü üstbilgisi unutmayın.

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. Merhaba tanılama profili Bu günlükler tooput istediğiniz yere tooselect hello depolama hesabını etkinleştirir.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

Örnek bir sanal makine önyükleme tanılaması etkin, burada bizim depodaki kullanıma toodeploy.

## <a name="update-an-existing-virtual-machine"></a>Mevcut bir sanal makineyi güncelleştirme ##

tooenable önyükleme tanılaması hello Portal aracılığıyla, mevcut bir sanal makine hello Portal aracılığıyla güncelleştirebilirsiniz. Select hello önyükleme tanılaması seçeneği ve kaydedin. Merhaba VM tootake etkisi yeniden başlatın.

![Mevcut VM’yi güncelleştirme](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

