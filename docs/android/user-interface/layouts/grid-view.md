---
title: GridView
ms.prod: xamarin
ms.assetid: 6992C4FF-ECBB-3493-AEE6-3E063C1A8C54
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 02/06/2018
ms.openlocfilehash: 82c82de912fd253d45e6343e2dd1c50e389c6371
ms.sourcegitcommit: 945df041e2180cb20af08b83cc703ecd1aedc6b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/04/2018
ms.locfileid: "30766295"
---
# <a name="gridview"></a>GridView

[`GridView`](https://developer.xamarin.com/api/type/Android.Widget.GridView/) 是[ `ViewGroup` ](https://developer.xamarin.com/api/type/Android.Views.ViewGroup/)二維度的可捲動方格中顯示的項目。 方格項目會自動插入至版面配置使用[ `ListAdapter` ](https://developer.xamarin.com/api/property/Android.App.ListActivity.ListAdapter/)。

在本教學課程中，您將建立方格的影像縮圖。 選取項目時，快顯通知訊息會顯示映像的位置。

啟動新的專案，名為**HelloGridView**。

尋找您想要使用時，某些相片或[下載這些範例影像](http://developer.android.com/shareables/sample_images.zip)。 將影像檔加入至專案的**資源/Drawable**目錄。 在**屬性**視窗中，針對每個要設定建置動作**AndroidResource**。

開啟**Resources/Layout/Main.axml**檔案，並插入下列：

```xml
<?xml version="1.0" encoding="utf-8"?>
<GridView xmlns:android="http://schemas.android.com/apk/res/android"
    android:id="@+id/gridview"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:columnWidth="90dp"
    android:numColumns="auto_fit"
    android:verticalSpacing="10dp"
    android:horizontalSpacing="10dp"
    android:stretchMode="columnWidth"
    android:gravity="center"
/>
```

這[ `GridView` ](https://developer.xamarin.com/api/type/Android.Widget.GridView/)會填滿整個螢幕。 屬性是而本身的說明性。 如需有效的屬性的詳細資訊，請參閱[ `GridView` ](https://developer.xamarin.com/api/type/Android.Widget.GridView/)參考。

開啟`HelloGridView.cs`插入下列程式碼和[ `OnCreate()` ](https://developer.xamarin.com/api/member/Android.App.Activity.OnCreate/p/Android.OS.Bundle/)方法：

```csharp
protected override void OnCreate (Bundle bundle)
{
    base.OnCreate (bundle);

    SetContentView (Resource.Layout.Main);

    var gridview = FindViewById<GridView> (Resource.Id.gridview);
    gridview.Adapter = new ImageAdapter (this);

    gridview.ItemClick += delegate (object sender, AdapterView.ItemClickEventArgs args) {
        Toast.MakeText (this, args.Position.ToString (), ToastLength.Short).Show ();
    };
}
```

之後**Main.axml**版面配置 設定的內容檢視中， [ `GridView` ](https://developer.xamarin.com/api/type/Android.Widget.GridView/)擷取自版面配置與[ `FindViewById` ](https://developer.xamarin.com/api/member/Android.App.Activity.FindViewById/)。 [ `Adapter` ](https://developer.xamarin.com/api/property/Android.Widget.AdapterView.RawAdapter/)屬性然後用來設定自訂的配接器 (`ImageAdapter`) 做為來源，會顯示在方格的所有項目。 `ImageAdapter`會在下一個步驟中建立。

若要在按一下方格中的項目時，請執行一些動作，在匿名委派訂閱[ `ItemClick` ](https://developer.xamarin.com/api/event/Android.Widget.AdapterView.ItemClick/)事件。
它會顯示[ `Toast` ](https://developer.xamarin.com/api/type/Android.Widget.Toast/)會顯示選取的項目 （以零為起始） 的索引位置 （在真實世界案例中，位置無法用來取得完整大小的映像的其他工作）。 請注意 Java 樣式接聽程式的類別可以代替.NET 事件。

建立新的類別稱為`ImageAdapter`該子類別[ `BaseAdapter` ](https://developer.xamarin.com/api/type/Android.Widget.BaseAdapter/):

```csharp
public class ImageAdapter : BaseAdapter
{
    Context context;

    public ImageAdapter (Context c)
    {
        context = c;
    }

    public override int Count {
        get { return thumbIds.Length; }
    }

    public override Java.Lang.Object GetItem (int position)
    {
        return null;
    }

    public override long GetItemId (int position)
    {
        return 0;
    }

    // create a new ImageView for each item referenced by the Adapter
    public override View GetView (int position, View convertView, ViewGroup parent)
    {
        ImageView imageView;

        if (convertView == null) {  // if it's not recycled, initialize some attributes
            imageView = new ImageView (context);
            imageView.LayoutParameters = new GridView.LayoutParams (85, 85);
            imageView.SetScaleType (ImageView.ScaleType.CenterCrop);
            imageView.SetPadding (8, 8, 8, 8);
        } else {
            imageView = (ImageView)convertView;
        }

        imageView.SetImageResource (thumbIds[position]);
        return imageView;
    }

    // references to our images
    int[] thumbIds = {
        Resource.Drawable.sample_2, Resource.Drawable.sample_3,
        Resource.Drawable.sample_4, Resource.Drawable.sample_5,
        Resource.Drawable.sample_6, Resource.Drawable.sample_7,
        Resource.Drawable.sample_0, Resource.Drawable.sample_1,
        Resource.Drawable.sample_2, Resource.Drawable.sample_3,
        Resource.Drawable.sample_4, Resource.Drawable.sample_5,
        Resource.Drawable.sample_6, Resource.Drawable.sample_7,
        Resource.Drawable.sample_0, Resource.Drawable.sample_1,
        Resource.Drawable.sample_2, Resource.Drawable.sample_3,
        Resource.Drawable.sample_4, Resource.Drawable.sample_5,
        Resource.Drawable.sample_6, Resource.Drawable.sample_7
    };
}
```

首先，這會實作一些需要的方法繼承自[ `BaseAdapter` ](https://developer.xamarin.com/api/type/Android.Widget.BaseAdapter/)。 建構函式和[ `Count` ](https://developer.xamarin.com/api/property/Android.Widget.BaseAdapter.Count/)屬性都一目了然。 一般來說， [ `GetItem(int)` ](https://developer.xamarin.com/api/member/Android.Widget.BaseAdapter.GetItem/)應該會傳回實際物件的介面卡，指定的位置，但此範例中會忽略它。 同樣地， [ `GetItemId(int)` ](https://developer.xamarin.com/api/member/Android.Widget.BaseAdapter.GetItemId/)應該會傳回資料列識別碼的項目，但這裡不需要。

必要的第一個方法是[ `GetView()` ](https://developer.xamarin.com/api/member/Android.Widget.BaseAdapter.GetView/)。
這個方法會建立新[ `View` ](https://developer.xamarin.com/api/type/Android.Views.View/)每個映像新增至`ImageAdapter`。 此呼叫時， [ `View` ](https://developer.xamarin.com/api/type/Android.Views.View/)傳遞中，也就是正常回收的物件 (至少這一次呼叫之後)，因此沒有檢查物件是否為 null。 如果它*是*null [ `ImageView` ](https://developer.xamarin.com/api/type/Android.Widget.ImageView/)是具現化，而且想要的屬性，映像簡報設定：

- [`LayoutParams`](https://developer.xamarin.com/api/property/Android.Views.View.LayoutParameters/) 檢視設定的高度和寬度&mdash;這樣可以確保，無論 drawable 的大小，每個影像會調整大小裁剪以納入這些維度，視需要。

- [`SetScaleType()`](https://developer.xamarin.com/api/member/Android.Widget.ImageView.SetScaleType/) 宣告的映像應該會從向中央 （如有必要）。

- [`SetPadding(int, int, int, int)`](https://developer.xamarin.com/api/member/Android.Views.View.SetPadding/) 定義所有側邊的邊框間距。 （請注意，是否映像有不同的外觀比例，然後較少的填補可能會造成更多裁剪影像的如果不符合提供給 ImageView 維度）。

如果[ `View` ](https://developer.xamarin.com/api/type/Android.Views.View/)傳遞至[ `GetView()` ](https://developer.xamarin.com/api/member/Android.Widget.BaseAdapter.GetView/)是*不*null，則本機[ `ImageView` ](https://developer.xamarin.com/api/type/Android.Widget.ImageView/)初始化回收[ `View` ](https://developer.xamarin.com/api/type/Android.Views.View/)物件。

在結尾[ `GetView()` ](https://developer.xamarin.com/api/member/Android.Widget.BaseAdapter.GetView/)方法，`position`整數傳遞至方法用來選取映像從`thumbIds`陣列，它會設定為映像資源[ `ImageView`](https://developer.xamarin.com/api/type/Android.Widget.ImageView/).

剩下的是定義`thumbIds`drawable 資源的陣列。

執行應用程式。 格線配置看起來應該像這樣：

[![顯示 15 影像的 GridView 的範例螢幕擷取畫面](grid-view-images/helloviews4.png)](grid-view-images/helloviews4.png#lightbox)

嘗試使用的行為[ `GridView` ](https://developer.xamarin.com/api/type/Android.Widget.GridView/)和[ `ImageView` ](https://developer.xamarin.com/api/type/Android.Widget.ImageView/)藉由調整其屬性的項目。 例如，而不是使用[ `LayoutParams` ](https://developer.xamarin.com/api/property/Android.Views.View.LayoutParameters/)請嘗試使用[ `SetAdjustViewBounds()` ](https://developer.xamarin.com/api/member/Android.Widget.ImageView.SetAdjustViewBounds/)。


## <a name="references"></a>參考

-   [`GridView`](https://developer.xamarin.com/api/type/Android.Widget.GridView/) 
-   [`ImageView`](https://developer.xamarin.com/api/type/Android.Widget.ImageView/)
-   [`BaseAdapter`](https://developer.xamarin.com/api/type/Android.Widget.BaseAdapter/).

*此頁面上的部分是修改依據工作建立及 Android 的開放原始碼專案所共用，並依據條款中所述來使用*
[*Creative Commons 2.5 Attribution 授權*](http://creativecommons.org/licenses/by/2.5/).
