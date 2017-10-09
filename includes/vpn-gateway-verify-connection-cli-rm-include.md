Bağlantınızı hello kullanarak başarılı olduğunu doğrulayabilirsiniz [az ağ vpn bağlantısı Göster](/cli/azure/network/vpn-connection#show) komutu. Merhaba örnekte '--ad ' hello bağlantı tootest istediğiniz toohello adını gösterir. Hello bağlantı kuruldu, hello işlemi yürütülürken 'Bağlanıyor' bağlantı durumunu gösterir. Merhaba bağlantı kurulduktan sonra hello too'Connected durumuna '.

```azurecli
az network vpn-connection show --name VNet1toSite2 --resource-group TestRG1
```

