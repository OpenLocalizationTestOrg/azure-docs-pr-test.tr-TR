1. İçinde **Çözüm Gezgini**, hello projesine sağ tıklatın ve **Yayımla**. **Yeni Oluştur**'u seçin ve **Yayımla**'ya tıklayın. 

    ![Yeni işlev uygulaması oluşturma ve yayımlama](./media/functions-vstools-publish/functions-vstools-publish-new-function-app.png)

2. Visual Studio tooyour Azure hesabına bağlanmadıysanız, tıklatın **Hesap Ekle...** .  

3. Merhaba, **App Service Oluştur** iletişim, kullanım hello **barındırma** aşağıdaki tablonun belirtilen hello ayarları: 

    ![Azure yerel çalışma zamanı](./media/functions-vstools-publish/functions-vstools-publish.png)

    | Ayar      | Önerilen değer  | Açıklama                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Uygulama Adı** | Genel olarak benzersiz bir ad | Yeni işlev uygulamanızı benzersiz şekilde tanımlayan ad. |
    | **Abonelik** | Aboneliğinizi seçin | Hello Azure aboneliği toouse. |
    | **[Kaynak Grubu](../articles/azure-resource-manager/resource-group-overview.md)** | myResourceGroup |  İşlev uygulamanız hangi toocreate grubu hello kaynağının adı. |
    | **[App Service Planı](../articles/azure-functions/functions-scale.md)** | Tüketim planı | Toochoose hello emin olun **tüketim** altında **boyutu** yeni bir plan oluşturduğunuzda.  |
    | **[Depolama hesabı](../articles/storage/common/storage-create-storage-account.md#create-a-storage-account)** | Genel olarak benzersiz bir ad | Mevcut bir depolama hesabını kullanın veya yeni bir hesap oluşturun.   |

4. Tıklatın **oluşturma** toocreate bu ayarlarla azure'da bir işlev uygulaması. Merhaba Sağlama tamamlandıktan sonra hello Not **Site URL'si** işlevi uygulamanızı azure'da hello adresidir değeri. 

    ![Azure yerel çalışma zamanı](./media/functions-vstools-publish/functions-vstools-publish-profile.png)
