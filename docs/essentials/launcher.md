---
title: Xamarin.Essentials 啟動器
description: Xamarin.Essentials 啟動器類別可讓應用程式來開啟系統的 URI。
ms.assetid: BABF40CC-8BEE-43FD-BE12-6301DF27DD33
author: jamesmontemagno
ms.author: jamont
ms.date: 07/25/2018
ms.openlocfilehash: 3ab820ece127558c1a5ca8b13c05fc4d6f20646e
ms.sourcegitcommit: 51c274f37369d8965b68ff587e1c2d9865f85da7
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/30/2018
ms.locfileid: "39353931"
---
# <a name="xamarinessentials-launcher"></a>Xamarin.Essentials： 啟動器

![發行前版本的 NuGet](~/media/shared/pre-release.png)

**啟動器**類別可讓您的應用程式，來開啟系統的 URI。 這是通常時使用深層連結到另一個應用程式的自訂 URI 配置。 如果您想要在瀏覽器開啟至網站，則您應該參閱**[瀏覽器](open-browser.md)** API。

## <a name="using-launcher"></a>使用啟動程式

在您的類別加入 Xamarin.Essentials 的參考：

```csharp
using Xamarin.Essentials;
```

若要使用啟動器功能呼叫`OpenAsync`方法並傳入`string`或`Uri`開啟。 （選擇性）`CanOpenAsync`方法可用來檢查裝置上的應用程式是否可由 URI 結構描述。

```csharp
public class LauncherTest
{
    public async Task OpenRideShare()
    {
        var supportsUri = await Launcher.CanOpenAsync("lyft://");
        if (supportsUri)
            await Launcher.OpenAsync("lyft://ridetype?id=lyft_line");
    }
}
```

## <a name="api"></a>API

- [啟動程式原始碼](https://github.com/xamarin/Essentials/tree/master/Xamarin.Essentials/Launcher)
- [啟動程式 API 文件](xref:Xamarin.Essentials.Launcher)
