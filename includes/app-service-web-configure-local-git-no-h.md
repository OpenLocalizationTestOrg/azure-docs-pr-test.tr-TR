Yerel Git dağıtım toohello web uygulaması ile Merhaba yapılandırma [az webapp dağıtım kaynağı config-yerel-git](/cli/azure/webapp/deployment/source#config-local-git) komutu.

Uygulama hizmeti çeşitli yolları toodeploy içerik tooa web uygulaması, FTP, yerel Git, GitHub, Visual Studio Team Services ve Bitbucket gibi destekler. Bu hızlı başlangıç için yerel Git’i kullanarak dağıtım gerçekleştirirsiniz. Azure yerel deposu tooa depodan Git komut toopush kullanarak dağıtma anlamına gelir. 

Komut, aşağıdaki Hello yerine  *\<app_name >* web uygulamanızın ada sahip.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

Merhaba çıktı biçimi aşağıdaki hello sahiptir:

```bash
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git
```

Merhaba `<username>` hello olan [dağıtım kullanıcı](#configure-a-deployment-user) bir önceki adımda oluşturduğunuz.

Merhaba gösterilen URI kopyalayın; Merhaba sonraki adımda kullanacaksınız.
