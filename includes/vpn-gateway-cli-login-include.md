Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin. Oturum açma hakkında daha fazla bilgi için bkz. [Azure CLI 2.0'ı kullanmaya başlama](/cli/azure/get-started-with-azure-cli).

```azurecli
az login
```

Birden fazla Azure aboneliğiniz varsa, hello hesap için hello abonelikleri listeler.

```azurecli
az account list --all
```

Merhaba abonelik toouse istediğinizi belirtin.

```azurecli
az account set --subscription <replace_with_your_subscription_id>
```