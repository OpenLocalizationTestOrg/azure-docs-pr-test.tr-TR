<span data-ttu-id="3ea3e-101">Hello Azure CLI tooget hello uzak dağıtım URL'si, API uygulaması için kullanın.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-101">Use hello Azure CLI tooget hello remote deployment URL for your API App.</span></span> <span data-ttu-id="3ea3e-102">Komut, aşağıdaki Hello yerine  *\<app_name >* web uygulamanızın ada sahip.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-102">In hello following command, replace *\<app_name>* with your web app's name.</span></span>

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup --query url --output tsv
```

<span data-ttu-id="3ea3e-103">Yerel Git dağıtım toobe mümkün toopush toohello uzak yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-103">Configure your local Git deployment toobe able toopush toohello remote.</span></span>

```bash
git remote add azure <URI from previous step>
```

<span data-ttu-id="3ea3e-104">Toohello Azure uzak toodeploy uygulamanızı iletin.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-104">Push toohello Azure remote toodeploy your app.</span></span> <span data-ttu-id="3ea3e-105">Merhaba dağıtım kullanıcı oluşturduğunuzda daha önce oluşturulan hello parolayı girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-105">You are prompted for hello password you created earlier when you created hello deployment user.</span></span> <span data-ttu-id="3ea3e-106">Daha önce hello hızlı başlangıcı oluşturduğunuz hello parola ve değil toolog toohello Azure portal kullanın hello parolayı girdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="3ea3e-106">Make sure that you enter hello password you created in earlier in hello quickstart, and not hello password you use toolog in toohello Azure portal.</span></span>

```bash
git push azure master
```
