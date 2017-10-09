1. Merhaba tıklatın **yeni** düğmesi hello sol üst köşesinin hello Azure portalı üzerinde bulunamadı.

1. **İşlem** > **İşlev Uygulaması**'na tıklayın ve **Aboneliğinizi** seçin. Ardından, hello tabloda belirtildiği gibi hello işlevi uygulama ayarlarını kullanın.

    ![Hello Azure portal işlev uygulaması oluşturma](./media/functions-create-function-app-portal/function-app-create-flow.png)

    | Ayar      | Önerilen değer  | Açıklama                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Uygulama adı** | Genel olarak benzersiz bir ad | Yeni işlev uygulamanızı tanımlayan ad. | 
    | **[Kaynak Grubu](../articles/azure-resource-manager/resource-group-overview.md)** |  myResourceGroup | Merhaba yeni kaynak grubunda hangi toocreate için işlevi uygulamanızı adlandırın. | 
    | **[Barındırma planı](../articles/azure-functions/functions-scale.md)** |   Tüketim planı | Tooyour işlev uygulaması kaynaklarının nasıl ayrıldığını tanımlar barındırma planı. Merhaba varsayılan **tüketim planlama**, kaynakları işlevlerinizi gerektirdiği gibi dinamik olarak eklenir. Yalnızca işlevlerinizi hello çalıştırdığınızda için ödeme yaparsınız.   |
    | **Konum** | Batı Avrupa | Kendinize veya işlevinizin erişeceği diğer hizmetlere yakın bir konum seçin. |
    | **[Depolama hesabı](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** |  Genel olarak benzersiz bir ad |  Merhaba işlevi uygulamanız tarafından kullanılan yeni depolama hesabı adı. Depolama hesabı adları 3 ile 24 karakter arasında olmalı ve yalnızca sayıyla küçük harf içermelidir. Var olan bir hesabı da kullanabilirsiniz. |

1. Tıklatın **oluşturma** tooprovision ve hello yeni işlev uygulaması dağıtın.
