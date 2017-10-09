## <a name="set-up-azure-cli-for-azure-dns"></a>Azure DNS için Azure CLI'yi ayarlama

### <a name="before-you-begin"></a>Başlamadan önce

Yapılandırmanıza başlamadan önce aşağıdaki öğelerindeki hello sahip olduğunuzu doğrulayın.

* Azure aboneliği. Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.
* Merhaba hello Azure CLI, Windows, Linux veya Mac için kullanılabilir en son sürümünü yükleyin Daha fazla bilgi için bkz. [yükleme hello Azure CLI](../articles/cli-install-nodejs.md).

### <a name="sign-in-tooyour-azure-account"></a>Azure hesabı tooyour içinde oturum

Bir konsol penceresi açın ve kimlik bilgilerinizi girerek kimliğinizi doğrulayın. Daha fazla bilgi için bkz: [tooAzure hello Azure CLI gelen oturum](../articles/xplat-cli-connect.md)

```azurecli
azure login
```

### <a name="switch-cli-mode"></a>CLI moduna geçme

Azure DNS, Azure Resource Manager'ı kullanır. CLI moduna toouse Azure Resource Manager komutları geçtiğinizden emin olun.

```azurecli
azure config mode arm
```

### <a name="select-hello-subscription"></a>Merhaba aboneliği seçin

Merhaba hesabının Hello abonelikleri kontrol edin.

```azurecli
azure account list
```

Azure abonelikleri toouse hangisinin seçin.

```azurecli
azure account set "subscription name"
```

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Azure Resource Manager, tüm kaynak gruplarının bir konum belirtmesini gerektirir. Bu kaynak grubundaki kaynaklar için hello varsayılan konum olarak kullanılır. Ancak, tüm DNS kaynakları global olduğundan, bölgesel değil, kaynak grubu konumu hello seçimine Azure DNS üzerinde hiçbir etkisi olmaz.

Var olan bir kaynak grubunu kullanıyorsanız bu adımı atlayabilirsiniz.

```azurecli
azure group create -n myresourcegroup --location "West US"
```

### <a name="register-resource-provider"></a>Kaynak sağlayıcısını kaydetme

Hello Azure DNS hizmeti hello Microsoft.Network kaynak sağlayıcısı tarafından yönetilir. Azure aboneliğinizde Azure DNS'yi kullanmadan önce bu kaynak sağlayıcısı kayıtlı toouse olmalıdır. Bu, her bir abonelik için tek seferlik bir işlemdir.

```azurecli
azure provider register --namespace Microsoft.Network
```

