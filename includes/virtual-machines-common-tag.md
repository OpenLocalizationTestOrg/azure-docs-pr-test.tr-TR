


## <a name="tagging-a-virtual-machine-through-templates"></a>Bir sanal makine şablonlarıyla etiketleme
İlk olarak, şablonları üzerinden etiketleme konumundaki bakalım. [Bu şablon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags) kaynakları aşağıdaki hello üzerinde etiketleri yerleştirir: işlem (sanal makine), depolama (depolama hesabı) ve ağ (genel IP adresi, sanal ağ ve ağ arabirimi). Bu şablon için bir Windows VM olmakla birlikte Linux VM'ler için uyarlanabilir.

Merhaba tıklatın **tooAzure dağıtmak** hello düğmesinden [şablon bağlantısı](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-tags). Bu toohello gideceği [Azure portal](https://portal.azure.com/) bu şablonu dağıtabileceğiniz.

![Etiketler basit dağıtımı](./media/virtual-machines-common-tag/deploy-to-azure-tags.png)

Bu şablon etiketleri aşağıdaki hello içerir: *departmanı*, *uygulama*, ve *oluşturan*. Ekle/hello şablonunda doğrudan bu etiketler farklı etiket adları isterseniz Düzenle.

![Bir şablonu Azure etiketleri](./media/virtual-machines-common-tag/azure-tags-in-a-template.png)

Gördüğünüz gibi hello etiketleri iki nokta (:) ayırarak anahtar/değer çiftleri olarak tanımlanır. Başlangıç etiketleri bu biçimde tanımlanmış olması gerekir:

        “tags”: {
            “Key1” : ”Value1”,
            “Key2” : “Value2”
        }

Tercih ettiğiniz hello etiketleriyle düzenlemeyi tamamladıktan sonra hello şablon dosyasını kaydedin.

Merhaba sonraki **parametreleri Düzenle** bölümünde etiketlerinizi için hello değerlere doldurabilirsiniz.

![Azure portalında etiket düzenleme](./media/virtual-machines-common-tag/edit-tags-in-azure-portal.png)

Tıklatın **oluşturma** toodeploy bu şablonla, etiket değeri.

## <a name="tagging-through-hello-portal"></a>Merhaba Portal etiketleme
Kaynaklarınızın etiketleriyle oluşturduktan sonra görüntülemek, ekleyin ve hello portal etiketleri silin.

Select hello simgesi tooview etiketlerinizi etiketler:

![Azure portalında etiketleri simgesi](./media/virtual-machines-common-tag/azure-portal-tags-icon.png)

Kendi anahtar/değer çifti tanımlayarak hello Portalı aracılığıyla yeni bir etiket eklemek ve kaydedin.

![Azure portalında Yeni Etiket Ekle](./media/virtual-machines-common-tag/azure-portal-add-new-tag.png)

Yeni etiket şimdi kaynağınız için etiketler hello listesinde gösterilmelidir.

![Azure portalında kaydedilen yeni etiket](./media/virtual-machines-common-tag/azure-portal-saved-new-tag.png)

