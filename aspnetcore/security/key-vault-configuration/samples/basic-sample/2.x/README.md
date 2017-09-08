# <a name="key-vault-configuration-provider-sample-application-aspnet-core-2x"></a><span data-ttu-id="59b49-101">Образец приложения поставщика конфигурации хранилища ключей (ASP.NET Core 2.x)</span><span class="sxs-lookup"><span data-stu-id="59b49-101">Key Vault Configuration Provider sample application (ASP.NET Core 2.x)</span></span>

<span data-ttu-id="59b49-102">В этом примере описывается использование поставщика конфигурации хранилища ключей Azure для ASP.NET Core 2.x.</span><span class="sxs-lookup"><span data-stu-id="59b49-102">This sample illustrates the use of the Azure Key Vault Configuration Provider for ASP.NET Core 2.x.</span></span> <span data-ttu-id="59b49-103">Пример 1.x ASP.NET Core см. в разделе [образец приложения поставщика конфигурации хранилища ключей (ASP.NET Core 1.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples/basic-sample/1.x).</span><span class="sxs-lookup"><span data-stu-id="59b49-103">For the ASP.NET Core 1.x sample, see [Key Vault Configuration Provider sample application (ASP.NET Core 1.x)](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/key-vault-configuration/samples/basic-sample/1.x).</span></span>

<span data-ttu-id="59b49-104">Дополнительные сведения о том, как работает этот пример см. в разделе [конфигурации поставщика хранилища ключей Azure](xref:security/key-vault-configuration) раздела.</span><span class="sxs-lookup"><span data-stu-id="59b49-104">For more information on how the sample works, see the [Azure Key Vault configuration provider](xref:security/key-vault-configuration) topic.</span></span>

## <a name="using-the-sample"></a><span data-ttu-id="59b49-105">Использование образца</span><span class="sxs-lookup"><span data-stu-id="59b49-105">Using the sample</span></span>
1. <span data-ttu-id="59b49-106">Создание хранилища ключей и настроить Azure Active Directory (Azure AD) для приложения согласно инструкциям в [приступить к работе с хранилищем ключей Azure](https://azure.microsoft.com/documentation/articles/key-vault-get-started/).</span><span class="sxs-lookup"><span data-stu-id="59b49-106">Create a key vault and set up Azure Active Directory (Azure AD) for the application following the guidance in [Get started with Azure Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/).</span></span>
  * <span data-ttu-id="59b49-107">Добавьте секреты в хранилище ключей с использованием [модуль AzureRM ключ хранилища PowerShell](/powershell/module/azurerm.keyvault) доступны из [коллекции PowerShell](https://www.powershellgallery.com/packages/AzureRM.KeyVault), [API REST хранилища ключей Azure](/rest/api/keyvault/), или [Портал azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="59b49-107">Add secrets to the key vault using the [AzureRM Key Vault PowerShell Module](/powershell/module/azurerm.keyvault) available from the [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureRM.KeyVault), the [Azure Key Vault REST API](/rest/api/keyvault/), or the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="59b49-108">Секреты создаются как *вручную* или *сертификат* секретные данные.</span><span class="sxs-lookup"><span data-stu-id="59b49-108">Secrets are created as either *Manual* or *Certificate* secrets.</span></span> <span data-ttu-id="59b49-109">*Сертификат* секретные данные, сертификаты для использования приложений и служб, но не поддерживаются поставщиком конфигурации.</span><span class="sxs-lookup"><span data-stu-id="59b49-109">*Certificate* secrets are certificates for use by apps and services but are not supported by the configuration provider.</span></span> <span data-ttu-id="59b49-110">Следует использовать *вручную* параметр, чтобы создать секреты пары "имя значение" для использования с поставщиком конфигурации.</span><span class="sxs-lookup"><span data-stu-id="59b49-110">You should use the *Manual* option to create name-value pair secrets for use with the configuration provider.</span></span>
    * <span data-ttu-id="59b49-111">Простой секреты, создаются в виде пар "имя значение".</span><span class="sxs-lookup"><span data-stu-id="59b49-111">Simple secrets are created as name-value pairs.</span></span> <span data-ttu-id="59b49-112">Azure имена секрета хранилища ключей, ограничены буквы, цифры и дефисы.</span><span class="sxs-lookup"><span data-stu-id="59b49-112">Azure Key Vault secret names are limited to alphanumeric characters and dashes.</span></span>
    * <span data-ttu-id="59b49-113">Используйте иерархическими значениями (разделы конфигурации) `--` (двух дефисов) в качестве разделителя в образце.</span><span class="sxs-lookup"><span data-stu-id="59b49-113">Hierarchical values (configuration sections) use `--` (two dashes) as a separator in the sample.</span></span> <span data-ttu-id="59b49-114">Имена, которые обычно используются для разделения раздел из подраздела в [конфигурации ASP.NET Core](xref:fundamentals/configuration), не разрешены в именах секрета.</span><span class="sxs-lookup"><span data-stu-id="59b49-114">Colons, which are normally used to delimit a section from a subkey in [ASP.NET Core configuration](xref:fundamentals/configuration), aren't allowed in secret names.</span></span> <span data-ttu-id="59b49-115">Таким образом используются и при загрузке секреты в конфигурации приложения для двоеточие местами двух дефисов.</span><span class="sxs-lookup"><span data-stu-id="59b49-115">Therefore, two dashes are used and swapped for a colon when the secrets are loaded into the app's configuration.</span></span>
    * <span data-ttu-id="59b49-116">Создайте два *вручную* секреты с помощью следующих пар имя значение.</span><span class="sxs-lookup"><span data-stu-id="59b49-116">Create two *Manual* secrets with the following name-value pairs.</span></span> <span data-ttu-id="59b49-117">Первый секретный код является простым именем и значением и второй секретный код создает секретное значение с раздел и раздел имя секрета:</span><span class="sxs-lookup"><span data-stu-id="59b49-117">The first secret is a simple name and value, and the second secret creates a secret value with a section and subkey in the secret name:</span></span>
      * <span data-ttu-id="59b49-118">`SecretName`: `secret_value_1`</span><span class="sxs-lookup"><span data-stu-id="59b49-118">`SecretName`: `secret_value_1`</span></span>
      * <span data-ttu-id="59b49-119">`Section--SecretName`: `secret_value_2`</span><span class="sxs-lookup"><span data-stu-id="59b49-119">`Section--SecretName`: `secret_value_2`</span></span>
  * <span data-ttu-id="59b49-120">Регистрация примера приложения в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="59b49-120">Register the sample app with Azure Active Directory.</span></span>
  * <span data-ttu-id="59b49-121">Разрешить приложению доступ к хранилища ключей.</span><span class="sxs-lookup"><span data-stu-id="59b49-121">Authorize the app to access the key vault.</span></span> <span data-ttu-id="59b49-122">При использовании `Set-AzureRmKeyVaultAccessPolicy` командлет PowerShell, чтобы разрешить приложению доступ к хранилища ключей, обеспечивают `List` и `Get` доступ к секретной информации с `-PermissionsToKeys list,get`.</span><span class="sxs-lookup"><span data-stu-id="59b49-122">When you use the `Set-AzureRmKeyVaultAccessPolicy` PowerShell cmdlet to authorize the app to access the key vault, provide `List` and `Get` access to secrets with `-PermissionsToKeys list,get`.</span></span>
2. <span data-ttu-id="59b49-123">Обновление приложения *appsettings.json* файл со значениями `Vault`, `ClientId`, и `ClientSecret`.</span><span class="sxs-lookup"><span data-stu-id="59b49-123">Update the app's *appsettings.json* file with the values of `Vault`, `ClientId`, and `ClientSecret`.</span></span>
3. <span data-ttu-id="59b49-124">Запустите пример приложения, который получает свои значения конфигурации `IConfigurationRoot` с тем же именем, как имя секрета.</span><span class="sxs-lookup"><span data-stu-id="59b49-124">Run the sample app, which obtains its configuration values from `IConfigurationRoot` with the same name as the secret name.</span></span>
  * <span data-ttu-id="59b49-125">Не иерархическими значениями: значение для `SecretName` получен с `config["SecretName"]`.</span><span class="sxs-lookup"><span data-stu-id="59b49-125">Non-hierarchical values: The value for `SecretName` is obtained with `config["SecretName"]`.</span></span>
  * <span data-ttu-id="59b49-126">Иерархическими значениями (разделов): используйте `:` нотации (двоеточие) или `GetSection` метода расширения.</span><span class="sxs-lookup"><span data-stu-id="59b49-126">Hierarchical values (sections): Use `:` (colon) notation or the `GetSection` extension method.</span></span> <span data-ttu-id="59b49-127">Выполните один из этих подходов, чтобы получить значение конфигурации.</span><span class="sxs-lookup"><span data-stu-id="59b49-127">Use either of these approaches to obtain the configuration value:</span></span>
    * `config["Section:SecretName"]`
    * `config.GetSection("Section")["SecretName"]`