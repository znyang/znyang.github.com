## 概述

视图布局(View Layouts)是一种视图类，主要用于组织和定位视图控件。这些布局类（LinearLayout，RelativeLayout等等）用于显示子控件，例如屏幕上的文本控件、按钮。
Android中的Activity(页面)使用布局作为容器视图控件，也可以很好的包含其他嵌套布局。几乎所有的Activity都有布局容器，类似于大多数HTML中使用"div"来包含其他内容的方式一样。

有几个很常用的布局，然后许多是用于仅非常特别的情况下才使用的专用布局。主要的布局有**LinearLayout**，**RelativeLayout**，**FrameLayout**等等。

重要的是要注意这些视图布局的类层次结构。Layout是ViewGroup的之类，而ViewGroup是View的之类。这意味着将Layout(例如LinearLayout)当作一个View参数来使用是完全可以的。ViewGroup中还包含一个内部静态类LayoutParams，用于在代码中创建或编辑布局。请记住，ViewGroup的每个之类，都有自己的内部静态类LayoutParams，他们是ViewGroup.LayoutParams的之类。当初学者在使用代码来创建视图布局是，往往会迷惑于不同的LayoutParams的使用，导致出现很多不好发现的问题。

## LinearLayout (线性布局)

线性布局(LinearLayout)就像它的名字一样，所有的元素显示在一个单一的方向上（*horizontally*或*vertically*），可以在`LinearLayout`节点上指定`android:orientation`属性来修改方向。

All children of a LinearLayout are displayed sequentially based on the order they are defined within the layout. A LinearLayout respects *margins* between children and the *gravity* (right, center, or left alignment) of each child.

普通的View在LinearLayout中常用的属性有:

 * `android:gravity` - 控制View中内容的对齐方式
 * `android:layout_gravity` - 控制该View在父容器中的对齐方式
 * `android:layout_weight` - 指定额外空间分配给当前的View [extra space in the layout](http://developer.android.com/guide/topics/ui/layout/linear.html#Weight) 

LinearLayout 示例代码段:

```xml
<?xml version="1.0" encoding="utf-8"?>
<!-- Parent linear layout with vertical orientation -->
<LinearLayout
  xmlns:android="http://schemas.android.com/apk/res/android"
  android:orientation="vertical"
  android:layout_width="match_parent"
  android:layout_height="match_parent">
   
  <TextView android:layout_width="match_parent" 
			android:layout_height="wrap_content"
            android:text="Email:"
			android:padding="5dp"/>
             
  <EditText android:layout_width="match_parent" 
			android:layout_height="wrap_content"
            android:layout_marginBottom="10dp"/>            
</LinearLayout>
```

## RelativeLayout

In a relative layout every element arranges itself relative to other elements or a parent element. RelativeLayout positions views based on a number of directional attributes:

* Position based on siblings: *layout_above*, *layout_below*, *layout_toLeftOf*, *layout_toRightOf*
* Position based on parent: *layout_alignParentTop*, *layout_alignParentBottom*, *layout_alignParentLeft*, *layout_alignParentRight*, *android:layout_centerHorizontal*, *android:layout_centerVertical*
* Alignment based on siblings: *layout_alignTop*, *layout_alignBottom*, *layout_alignLeft*, *layout_alignRight*, *layout_alignBaseline*

An example of a RelativeLayout:

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
                android:layout_width="match_parent"
                android:layout_height="wrap_content">
 
    <TextView android:id="@+id/label" android:layout_width="match_parent"
              android:layout_height="wrap_content" android:text="Email" />
 
    <EditText android:id="@+id/inputEmail" android:layout_width="match_parent"
              android:layout_height="wrap_content" android:layout_below="@id/label" />
   
    <Button android:id="@+id/btnLogin" android:layout_width="wrap_content"
            android:layout_height="wrap_content" android:layout_below="@id/inputEmail"
            android:layout_alignParentLeft="true" android:layout_marginRight="5dp"
            android:text="Login" />
</RelativeLayout>
```

You can see more about this layout by inspecting the [RelativeLayout.LayoutParams](http://developer.android.com/reference/android/widget/RelativeLayout.LayoutParams.html) docs and the official [RelativeLayout guide](http://developer.android.com/guide/topics/ui/layout/relative.html).

## FrameLayout

In a frame layout, the children are displayed with a z-index in the order of how they appear.  Put simply, the last child added to a `FrameLayout` will be drawn on top of all the previous children.  Think of it like a stack of items, the item last put on the stack will be drawn on top of the items below it.  This layout makes it very easy to draw on top of other layouts, especially for tasks such as button placement. 

To arrange the children inside of a `FrameLayout` use the `android:gravity` attribute along with whatever `android:padding` and `android:margin` you need. 

Example of FrameLayout snippet:
```xml
<FrameLayout
    android:id="@+id/frame_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
    <!-- Child1 is drawn first -->
    <ImageView
        android:id="@+id/child1"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:contentDescription="Image"
        android:src="@drawable/icon" />
    <!-- Child2 is drawn over Child1 -->
    <TextView
        android:id="@+id/child2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Child 2"
        android:layout_gravity="top|left" />
    <!-- Child3 is drawn over Child1 and Child2 -->
    <TextView
        android:id="@+id/child3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Child 3"
        android:layout_gravity="top|right" />
</FrameLayout>
```

In this example, an `ImageView` is set to the full size of the `FrameLayout`.  We then draw two `TextView`'s over it.

## Optimizing Layout Performance

To optimize layout performance, minimize the number of instantiated layouts and especially minimize deep nested layouts whenever possible. This is why you should generally use a `RelativeLayout` whenever possible instead of nested `LinearLayout`. Review the following references for more detail on optimizing your view hierarchy:

- [Android Layout Tricks](http://android-developers.blogspot.ca/2009/02/android-layout-tricks-1.html?m=1)
- [Optimizing Layouts](http://developer.android.com/training/improving-layouts/optimizing-layout.html)
- [Layout Optimization](http://code.tutsplus.com/tutorials/android-sdk-tools-layout-optimization--mobile-5245)

## References

 * <http://developer.android.com/guide/topics/ui/declaring-layout.html>
 * <http://developer.android.com/guide/topics/ui/layout/linear.html>
 * <http://developer.android.com/guide/topics/ui/layout/relative.html>
 * <http://www.learn-android.com/2010/01/05/android-layout-tutorial/>
 * <http://mobile.tutsplus.com/tutorials/android/android-layout/>
 * <http://www.androidhive.info/2011/07/android-layouts-linear-layout-relative-layout-and-table-layout/>
 * <http://logc.at/2011/10/18/when-to-use-linearlayout-vs-relativelayout/>
 * <http://developer.android.com/reference/android/widget/FrameLayout.html>