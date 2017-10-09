Hello Azure CLI tooget hello uzak dağıtım URL'si, API uygulaması için kullanın. Komut, aşağıdaki Hello yerine  *\<app_name >* web uygulamanızın ada sahip.

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

Yerel Git dağıtım toobe mümkün toopush toohello uzak yapılandırın.

```bash
git remote add azure <URI from previous step>
```

Toohello Azure uzak toodeploy uygulamanızı iletin. Merhaba dağıtım kullanıcı oluşturduğunuzda daha önce oluşturulan hello parolayı girmeniz istenir. Daha önce hello hızlı başlangıcı oluşturduğunuz hello parola ve değil toolog toohello Azure portal kullanın hello parolayı girdiğinizden emin olun.

```bash
git push azure master
```
