---
title: 如何設定 Xamarin Studio 中的 Mono 執行階段環境變數，針對 iOS 專案？
ms.topic: troubleshooting
ms.prod: xamarin
ms.assetid: 1176CEA9-C7F1-411B-8F1A-99374E8AFF33
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/31/2017
ms.openlocfilehash: 5f4f3a2de012d35ddca9c1fa830d599d9d5acb17
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
ms.locfileid: "30776114"
---
# <a name="how-do-i-set-mono-runtime-environment-variables-for-ios-projects-in-xamarin-studio"></a>如何設定 Xamarin Studio 中的 Mono 執行階段環境變數，針對 iOS 專案？

如果您需要為單聲道設定任何執行階段環境變數，您可以設定**專案選項 > 執行 > 一般**頁面。

附註： SGen 回收環境變數 (MONO\_GC\_PARAMS) 從 Xamarin Studio 啟動時，才會使用這種方式的設定。 如果您啟動來自裝置的應用程式，將忽略 Sgen 的設定。 

若要永久設定應用程式的環境變數，您需要加入這當做其他 mtouch 引數 （適用於所有相關的設定）：

```csharp
   --setenv=NAME=VALUE
```

若要查看可以設定環境變數，請參閱單聲道 man 頁面： [ http://docs.go-mono.com/?link=man%3amono(1) ](http://docs.go-mono.com/?link=man%3amono(1))請參閱一節： `ENVIRONMENT VARIABLES`

![](xs-mono-runtime-images/environment-variables.jpg "設定專案的環境變數")
