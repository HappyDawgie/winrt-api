---
-api-id: T:Windows.UI.Xaml.Controls.Page
-api-type: winrt class
---

<!-- Class syntax.
public class Page : Windows.UI.Xaml.Controls.UserControl, Windows.UI.Xaml.Controls.IPage, Windows.UI.Xaml.Controls.IPageOverrides
-->

# Windows.UI.Xaml.Controls.Page

## -description
Represents content that a [Frame](frame.md) control can navigate to.

## -xaml-syntax
```xaml
<Page .../>
-or-
<Page ...>
  singleRootElement
</Page>
```


## -remarks
The [Page](page.md) class encapsulates content that the [Frame](frame.md) control can navigate to. You will generally create your own page types that derive from the [Page](page.md) class, and use [Page](page.md) (or a custom type) as the root element for the XAML-declared content.

[Page](page.md) is a [UserControl](usercontrol.md), therefore you can declare a single XAML object element as [Content](usercontrol_content.md) for the [Page](page.md). Most pages contain more than one UI element in total. You typically use a panel or items control as the immediate child of a [Page](page.md), so that you can have the page contain and compose multiple elements of a UI.

You can also specify app bars, with the [TopAppBar](page_topappbar.md) and [BottomAppBar](page_bottomappbar.md) properties. You must use property element syntax for these properties to contain the [AppBar](appbar.md) values in XAML.

You can create new pages using the **Add | New Item** menu option for your project in Microsoft Visual Studio. These all create XAML files where the root is a [Page](page.md) class, and the code-behind class derives from [Page](page.md). Some page item templates add navigation support and additional features. For more info on the Microsoft Visual Studio item templates, see [C#, VB, and C++ item templates for ](http://msdn.microsoft.com/library/02c61b49-894f-4aa6-827c-667772536976).

Create as many pages as you need to present the content in your app, and then navigate to those pages by calling the [Frame.Navigate](frame_navigate.md) method and passing in a type reference for the page to navigate to. By type reference, we mean an instance of a class that identifies a type in the type system, for the language you are using. For Microsoft .NET that type is [System.Type](https://msdn.microsoft.com/library/system.type.aspx), and you can get a [System.Type](https://msdn.microsoft.com/library/system.type.aspx) reference from a page class' name by using the operators **typeof** (C#) or **GetType** (Visual Basic). For Visual C++ component extensions (C++/CX), use [TypeName](../windows.ui.xaml.interop/typename.md). Initialize a [TypeName](../windows.ui.xaml.interop/typename.md) by using the **typeid** of a class. **typeid** is a component extension that can be called for any runtime class.

Through [Frame.Navigate](frame_navigate.md), you can also pass in a parameter object to initialize the page to a particular state. The parameter object is loosely typed but serialization of navigation history only works for basic types (see Remarks in [Frame.Navigate(Type, Object)](frame_navigate_1603787821.md)). Pages that are navigated to as part of an activation generally pass data from the activation. Other navigation scenarios such as search result pages also have expectations of what info will be contained in the parameter.

By default, each navigation creates a new instance of the specific [Page](page.md) (or subclass) requested, and disposes the previous page instance. This happens even when navigating back to a previously visited page or when the new page type is the same as the previous page type. Apps that involve frequent navigation to the same pages can cache and reuse the page instances to make navigation more efficient. To do this, set the [Frame.CacheSize](frame_cachesize.md) property to specify how many pages to cache. For each page type that you want to cache, you must also set the [NavigationCacheMode](page_navigationcachemode.md) property to either **Enabled** or **Required**. Pages with a **Required** cache mode are cached regardless of the [CacheSize](frame_cachesize.md) value, and do not count against the [CacheSize](frame_cachesize.md) total.

You can override the page [OnNavigatedTo](page_onnavigatedto.md), [OnNavigatingFrom](page_onnavigatingfrom.md), and [OnNavigatedFrom](page_onnavigatedfrom.md) methods to perform tasks such as initializing and saving the page state. [OnNavigatingFrom](page_onnavigatingfrom.md) can be used to cancel a navigation by setting a [Cancel](../windows.ui.xaml.navigation/navigatingcanceleventargs_cancel.md) property in the event data from your handler.

## -examples
The following code example shows an abridged version of the [OnLaunched](../windows.ui.xaml/application_onlaunched.md) method override generated for the blank application template in Visual Studio. This code shows how the content of the app window is set to a new [Frame](frame.md), which is then navigated to the default initial [Page](page.md).

```csharp
        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            Frame rootFrame = Window.Current.Content as Frame;
            if (rootFrame == null)
            {
                // Create a Frame to act as the navigation context and navigate to the first page
                rootFrame = new Frame();
                // Place the frame in the current Window
                Window.Current.Content = rootFrame;
            }
            if (rootFrame.Content == null)
            {
                // When the navigation stack isn't restored navigate to the first page,
                // configuring the new page by passing required information as a navigation
                // parameter
                rootFrame.Navigate(typeof(MainPage), e.Arguments);
            }
            // Ensure the current window is active
            Window.Current.Activate();
        }

```

```vbnet
    Protected Overrides Sub OnLaunched(e As Windows.ApplicationModel.Activation.LaunchActivatedEventArgs)
        Dim rootFrame As Frame = TryCast(Window.Current.Content, Frame)
        If rootFrame Is Nothing Then
            ' Create a Frame to act as the navigation context and navigate to the first page
            rootFrame = New Frame()
            ' Place the frame in the current Window
            Window.Current.Content = rootFrame
        End If
        If rootFrame.Content Is Nothing Then
            ' When the navigation stack isn't restored navigate to the first page,
            ' configuring the new page by passing required information as a navigation
            ' parameter
            rootFrame.Navigate(GetType(MainPage), e.Arguments)
        End If
        ' Ensure the current window is active
        Window.Current.Activate()
    End Sub

```

```cpp
void App::OnLaunched(Windows::ApplicationModel::Activation::LaunchActivatedEventArgs^ e)
{
    auto rootFrame = dynamic_cast<Frame^>(Window::Current->Content);
    if (rootFrame == nullptr)
    {
        rootFrame = ref new Frame();
        if (rootFrame->Content == nullptr)
        {
            // When the navigation stack isn't restored navigate to the first page,
            // configuring the new page by passing required information as a navigation
            // parameter
            rootFrame->Navigate(TypeName(MainPage::typeid), e->Arguments);
        }
        // Place the frame in the current Window
        Window::Current->Content = rootFrame;
        // Ensure the current window is active
        Window::Current->Activate(); 
    }
    //else case omitted
}
```

For example code that adds an [AppBar](appbar.md) to a page, see [Quickstart: adding app bars](http://msdn.microsoft.com/library/9915aea1-e738-4c4b-a838-85625055fa06) or [How to share an app bar across pages](http://msdn.microsoft.com/library/89d3e780-2c8d-4e4d-a0a9-ebf0be87a730). For example code that uses [NavigationCacheMode](page_navigationcachemode.md), see [Navigation](http://msdn.microsoft.com/library/742c1c18-c7b1-47b7-866c-726eeb8235ec) or [XAML Navigation sample](http://go.microsoft.com/fwlink/p/?LinkID=330214).



## -see-also
[Frame](frame.md), [UserControl](usercontrol.md), [Quickstart: adding app bars](http://msdn.microsoft.com/library/9915aea1-e738-4c4b-a838-85625055fa06), [Navigation design basics overview](https://docs.microsoft.com/windows/uwp/design/basics/navigation-basics), [XAML Navigation sample](http://go.microsoft.com/fwlink/p/?LinkID=330214)