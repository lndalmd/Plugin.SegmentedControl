# Plugin Segmented Control for Xamarin Forms and .NET Standard

[![NuGet Badge](https://buildstats.info/nuget/Plugin.SegmentedControl.Netstandard)](https://www.nuget.org/packages/Plugin.SegmentedControl.Netstandard/)

*Please star this project if you find it useful. Thank you!*

## Why
There are other Segmented Control libraries out there. This library adds two important capabilities:
- It works across all three key platforms: iOS, Android and UWP - all other libraries I've encounted lack UWP.
- It's based on .NET Standard

## Supported platforms
|Platform|Supported|Version|Renderer|
| ------------------- | :-----------: | :-----------: | :------------------: |
|Xamarin.iOS Unified|Yes|iOS 8.1+|UISegmentedControl|
|Xamarin.Android|Yes|API 26+|RadioGroup|
|Xamarin.UWP|Yes|Win10 16299+|User Control/RadioButton|
|Xamarin.MacOS|Yes|10.0+|NSSegmentedControl|

For previous versions of UWP please use version 1.1.5.

## How to used
Using this plugin is easy. 

### iOS
Add initializer to `AppDelegate`

```csharp
public override bool FinishedLaunching(UIApplication app, NSDictionary options)
{
    global::Xamarin.Forms.Forms.Init();

    SegmentedControlRenderer.Initialize();
    ...
}
```

### UWP

You need to add the assembly to App.xaml.cs in you project. For more details see the Xamarin documentation [here](https://developer.xamarin.com/guides/xamarin-forms/platform-features/windows/installation/universal/#Troubleshooting).

```csharp
var assembliesToInclude = new List<Assembly> {typeof(SegmentedControlRenderer).GetTypeInfo().Assembly};

Xamarin.Forms.Forms.Init(e, assembliesToInclude);
```

### Android
No special needs.

For using custom fonts with Android see this blog post: [https://blog.verslu.is/xamarin/xamarin-forms-xamarin/custom-fonts-with-xamarin-forms-revisited/](https://blog.verslu.is/xamarin/xamarin-forms-xamarin/custom-fonts-with-xamarin-forms-revisited/)

#### .NET Standard
The Xamarin Forms must use .NET Standard. I suggest using .NET Standard 2.0+. 

Here is a great blog post about how to move your PCL to .NET Standard: [Building Xamarin.Forms Apps with .NET Standard](https://blog.xamarin.com/building-xamarin-forms-apps-net-standard/)

#### XAML
![Plugin Segmented Control Picture](https://github.com/1iveowl/Plugin.SegmentedControl/blob/master/src/asset/SegmentedRadioButtonControl-1.png "Plugin Segmented Control")


```xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:Test.SegmentedControl"
             xmlns:control="clr-namespace:Plugin.Segmented.Control;assembly=Plugin.Segmented"
             x:Class="Test.SegmentedControl.MainPage">

    <ContentPage.Resources>
        <OnPlatform x:Key="PlatformFontName" x:TypeArguments="x:String">
            <On Platform="UWP" Value="Courier New"></On>
            <On Platform="Android" Value="as"></On>
            <On Platform="iOS" Value="trs"></On>
        </OnPlatform>
    </ContentPage.Resources>
    
    <ContentPage.Content>
        <StackLayout BackgroundColor="White" x:Name="SegmentWithStack">
            <Label 
                Text="Welcome to Xamarin.Forms!"
                HorizontalOptions="CenterAndExpand" />
            <control:SegmentedControl 
                x:Name="SegmentedControl" 
                SelectedSegment="{Binding SelectedSegment, Mode=TwoWay}"
                TintColor="BlueViolet"
                SelectedTextColor="White"
                DisabledColor="Gray"
                TextFontSize="12"
                TextFontFamily="{StaticResource PlatformFontName}"
                Margin="8,8,8,8"
                SegmentSelectedCommand="{Binding SegmentChangedCommand}"
                OnElementChildrenChanging="OnElementChildrenChanging"
                ItemsSource="{Binding SegmentStringSource}">
                <!--<control:SegmentedControl.Children>
                    <control:SegmentedControlOption Text="{Binding ChangeText}"/>
                    <control:SegmentedControlOption Text="Item 2"/>
                    <control:SegmentedControlOption Text="Item 3"/>
                    <control:SegmentedControlOption Text="Item 4"/>
                </control:SegmentedControl.Children>-->
            </control:SegmentedControl>
            <Label x:Name="ChoiceLabel" Text="{Binding ChoiceText}"></Label>
            <ScrollView>
                <StackLayout Margin="24, 24, 24, 24">
                    <Button Text="Change First Item Text" Clicked="ChangeFirstText"/>
                    <Button Text="Remove" Clicked="Button_OnClicked"></Button>
                    <Button Text="Tint Color Change Button" Clicked="ButtonTintColor_OnClicked"></Button>
                    <Button Text="Selected Text Change Button" Clicked="ButtonSelectedTextColor_OnClicked"></Button>
                    <Button Text="Disable Segment Control" Clicked="Disable_OnClicked"></Button>
                    <Button Text="Enable Segment Control" Clicked="Enable_OnClicked"></Button>
                    <Button Text="Change Disabled Color" Clicked="ChangeDisabledColor_OnClicked"></Button>
                    <Button Text="Select Segment 3" Clicked="SelectSegment3"></Button>
                    <Button Text="Disable First Segment" Clicked="DisableFirstSegment_OnClicked"></Button>
                    <Button Text="Enable First Segment" Clicked="EnableFirstSegment_OnClicked"></Button>
                    <Button Text="Change ItemsSource" Command="{Binding ChangeItemsSourceCommand}"></Button>
                </StackLayout>
            </ScrollView>
        </StackLayout>
    </ContentPage.Content>
</ContentPage>

```

or

```xml
<control:SegmentedControl 
	x:Name="SegmentedControl" 
	SelectedSegment="{Binding SegmentSelection}" 
	OnSegmentSelected="SegmentedControl_OnValueChanged" 
	TintColor="BlueViolet"
	SelectedTextColor="White"
	DisabledColor="Gray"
	Margin="8,8,8,8"
	ItemsSource="{Binding ListOfSegmentTitles}">
</control:SegmentedControl>

```

You can bind to the SegmentSelectedCommand for notification in your view model when a segment change has occurred.
```xml
<control:SegmentedControl
    SegmentSelectedCommand="{Binding SegmentChangedCommand}"
</control:SegmentedControl>   
```

## Credits
For inspiration and for the Android and iOS part I'd like to thank Alex Rainman for his great work on [SegmentedControl.FormsPlugin](https://www.nuget.org/packages/SegmentedControl.FormsPlugin/).

Thank you to [rjantz3](https://github.com/rjantz3) for adding much requested features and enhancements to this control library.
