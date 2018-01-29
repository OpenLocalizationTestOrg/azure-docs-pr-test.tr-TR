Cloud Shell içinde [az webapp deployment user set](/cli/azure/webapp/deployment/user?view=azure-cli-latest#az_webapp_deployment_user_set) komutuyla dağıtım kimlik bilgileri oluşturun. Bir web uygulamasına FTP ve yerel Git dağıtımı için dağıtım kullanıcısı gereklidir. Kullanıcı adı ve parola, hesap düzeyindedir. _Bunlar Azure aboneliği kimlik bilgilerinizden farklıdır._

Aşağıdaki örnekte  *\<kullanıcı adı >* ve  *\<parola >* (köşeli ayraçlar dahil) yeni bir kullanıcı adı ve parola ile. Kullanıcı adı benzersiz olmalıdır. Parola, en az sekiz karakter uzunluğunda olma ve şu üç öğeyi de içermelidir: harf, rakam, sembol. 

```azurecli-interactive
az webapp deployment user set --user-name <username> --password <password>
```

` 'Conflict'. Details: 409` hatası alırsanız kullanıcı adını değiştirin. ` 'Bad Request'. Details: 400` hatası alırsanız daha güçlü bir parola kullanın.

Bu dağıtım kullanıcısını bir kez oluşturduktan sonra tüm Azure dağıtımlarınız için kullanabilirsiniz.

> [!NOTE]
> Kullanıcı adını ve parolayı kaydedin. Daha sonra web uygulamasının dağıtımı için bunlara ihtiyacınız olacaktır.
>
>
