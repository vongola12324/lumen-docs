# 發行說明

- [Lumen 5.2.0](#5.2.0)
- [Lumen 5.1.0](#5.1.0)
- [Lumen 5.0.4](#5.0.4)
- [Lumen 5.0 (Based On Laravel 5.0.x)](#5.0)

<a name="5.2.0"></a>
## Lumen 5.2.0

Lumen 5.2.0 升級了 framework，採用 Laravel 5.2 系列的元件，並對 Lumen 的基本理念和宗旨有著重大的改變。

### 限定無狀態 APIs

Lumen 5.2 意味著 slimming Lumen 上的一個改變，Lumen 將專注於無狀態的服務，例如：JSON APIs。**這也意味著，「sessions」及「views」將不再被 Lumen 支援。**如果你需要這些功能，那你應該使用完整的 Laravel framework！將 Lumen 應用程式升級到完整的 Laravel framework，基本上，你只需要將你的路由和類別複製到一個全新的 Laravel 專案中即可，因為 Lumen 和 Laravel 共用了許多相同的元件，你的類別應該是不需要任何修改的。

### 認證

因為 Sessions 不再被 Lumen 支援，認證程序必須使用 API tokens 或一些標頭(headers)在無狀態下完成。你可以完整的控制 `AuthServiceProvider` 中的整個認證流程。請參照 [認證文件](/docs/{{version}}/authentication) 了解相關訊息。

### 測試輔助方法

自從 Sessions 不再被 Lumen 支援，所有的表格交互測試輔助方法(testing helpers)已經被移除。不過 JSON APIs 的測試輔助方法仍然可以使用，請參照 [testing documentation](/docs/{{version}}/testing) 了解相關訊息。

<a name="5.1.0"></a>
## Lumen 5.1.0

Lumen 5.1.0 升級了 framework，採用 Laravel 5.1 系列的元件。Lumen 在這次的更新中提供了一些新的功能，例如：事件廣播(event broadcasting)、中介層參數(middleware parameters)及測試的改進。  
完整的 Laravel 5.1 發行說明請參考 [Laravel 文件](http://laravel.tw/docs/releases)。

<a name="5.0.4"></a>
## Lumen 5.0.4

當你的專案升級到 Lumen 5.0.4 時，你應該將 `bootstrap/app.php` 中的建立 Lumen 應用程式類別修改如下：

	$app = new Laravel\Lumen\Application(
		realpath(__DIR__.'/../')
	);

> **附註：** 這不是一個**必要**的更新，但是它可以防止一些使用 Artisan 指令及 PHP 內建的網站伺服器上的 bug。

<a name="5.0"></a>
## Lumen 5.0

Lumen 5.0 是 Lumen framework 的第一個發行版本，基於 Laravel 5.x 系列的 PHP 元件。
