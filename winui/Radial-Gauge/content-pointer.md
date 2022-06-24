---
layout: post
title: Content pointer in WinUI Radial Gauge control | Syncfusion
description: Learn here all about content pointer feature of Syncfusion WinUI Radial Gauge control with image, text and customization support.
platform: WinUI
control: SfRadialGauge
documentation: ug
---

# Content pointer in WinUI Radial Gauge

The [`ContentPointer`]() in [`SfRadialGauge`](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Gauges.SfRadialGauge.html) allows you to use any content as a pointer using the [`Content`]() property of it. 

**Add custom text as content pointer**

The following code sample demonstrate how to add a custom text as a content pointer.

{% tabs %}

{% highlight xaml %}

<gauge:SfRadialGauge>
    <gauge:SfRadialGauge.Axes>
        <gauge:RadialAxis>
            <gauge:RadialAxis.Pointers>
                <gauge:ContentPointer Value="60">
                    <gauge:ContentPointer.Content>
                        <Grid Background="Orange"
                              BorderBrush="Black"
                              BorderThickness="1"
                              CornerRadius="4">
                            <TextBlock Text="Syncfusion"
                                       Margin="2" />
                        </Grid>
                    </gauge:ContentPointer.Content>
                </gauge:ContentPointer>
            </gauge:RadialAxis.Pointers>
        </gauge:RadialAxis>
    </gauge:SfRadialGauge.Axes>
</gauge:SfRadialGauge>

{% endhighlight %}

{% highlight c# %}

SfRadialGauge sfRadialGauge = new SfRadialGauge();

RadialAxis radialAxis = new RadialAxis();
sfRadialGauge.Axes.Add(radialAxis);

ContentPointer contentPointer = new ContentPointer();
contentPointer.Value = 60;
Grid contentPointerRootChild = new Grid
{
    Background = new SolidColorBrush(Colors.Orange),
    BorderBrush = new SolidColorBrush(Colors.Black),
    BorderThickness = new Thickness { Bottom = 1, Left = 1, Right = 1, Top = 1 },
    CornerRadius = new CornerRadius { BottomLeft = 4, BottomRight = 4, TopLeft = 4, TopRight = 4 }
};
contentPointerRootChild.Children.Add(new TextBlock
{
    Text = "Syncfusion",
    Margin = new Thickness { Bottom = 2, Left = 2, Right = 2, Top = 2 }
});

contentPointer.Content = contentPointerRootChild;
radialAxis.Pointers.Add(contentPointer);

this.Content = sfRadialGauge;

{% endhighlight %}

{% endtabs %}

![WinUI Radial Gauge content pointer](images/content-pointer/default-content-pointer.png)

**Add image to content pointer**

The following code demonstrate how to use a `Image` as a content pointer.

{% tabs %}

{% highlight xaml %}

<gauge:SfRadialGauge>
    <gauge:SfRadialGauge.Axes>
        <gauge:RadialAxis>
            <gauge:RadialAxis.Pointers>
                <gauge:ContentPointer Value="60">
                    <gauge:ContentPointer.Content>
                        <Grid Background="Orange"
                              BorderBrush="Black"
                              BorderThickness="1"
                              CornerRadius="4">
                            <Image Source="pin.png" />
                        </Grid>
                    </gauge:ContentPointer.Content>
                </gauge:ContentPointer>
            </gauge:RadialAxis.Pointers>
        </gauge:RadialAxis>
    </gauge:SfRadialGauge.Axes>
</gauge:SfRadialGauge>

{% endhighlight %}

{% highlight c# %}

SfRadialGauge sfRadialGauge = new SfRadialGauge();

RadialAxis radialAxis = new RadialAxis();
sfRadialGauge.Axes.Add(radialAxis);

ContentPointer contentPointer = new ContentPointer();
contentPointer.Value = 60;
contentPointer.IsInteractive = true;
Grid contentPointerRootChild = new Grid
{
    Background = new SolidColorBrush(Colors.Orange),
    BorderBrush = new SolidColorBrush(Colors.Black),
    BorderThickness = new Thickness { Bottom = 1, Left = 1, Right = 1, Top = 1 },
    CornerRadius = new CornerRadius { BottomLeft = 4, BottomRight = 4, TopLeft = 4, TopRight = 4 }
};
contentPointerRootChild.Children.Add(new Image
{
    Source = "pin.png",
    Margin = new Thickness { Bottom = 2, Left = 2, Right = 2, Top = 2 }
});

contentPointer.Content = contentPointerRootChild;
radialAxis.Pointers.Add(contentPointer);

this.Content = sfRadialGauge;

{% endhighlight %}

{% endtabs %}

![Image as a content of content pointer in WinUI Radial Gauge](images/content-pointer/winui-radial-gauge-image-pointer.png)

## Position customization

The content pointer can be moved near or far from its actual position using the [`MarkerOffset`](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Gauges.MarkerPointer.html#Syncfusion_UI_Xaml_Gauges_MarkerPointer_MarkerOffset) and [`OffsetUnit`](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Gauges.MarkerPointer.html#Syncfusion_UI_Xaml_Gauges_MarkerPointer_OffsetUnit) properties. 

When you set [`OffsetUnit`](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Gauges.MarkerPointer.html#Syncfusion_UI_Xaml_Gauges_MarkerPointer_OffsetUnit) to pixel, the content pointer will be moved based on the pixel value. If you set [`OffsetUnit`](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Gauges.MarkerPointer.html#Syncfusion_UI_Xaml_Gauges_MarkerPointer_OffsetUnit) to factor, then provided factor will be multiplied with the axis radius value, and then the pointer will be moved to corresponding value. The default value of [`OffsetUnit`](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Gauges.MarkerPointer.html#Syncfusion_UI_Xaml_Gauges_MarkerPointer_OffsetUnit) is [`SizeUnit.Pixel`](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Gauges.SizeUnit.html#Syncfusion_UI_Xaml_Gauges_SizeUnit_Pixel).

{% tabs %}

{% highlight xaml %}

<gauge:SfRadialGauge>
    <gauge:SfRadialGauge.Axes>
        <gauge:RadialAxis>
            <gauge:RadialAxis.Pointers>
                <gauge:ContentPointer Value="60"
                                    MarkerOffset="-0.1"
                                    OffsetUnit="Factor">
                    <gauge:ContentPointer.Content>
                        <Grid Background="Orange"
                              BorderBrush="Black"
                              BorderThickness="1"
                              CornerRadius="4">
                            <TextBlock Text="60"
                                       Margin="2" />
                            <Image Source="">
                        </Grid>
                    </gauge:ContentPointer.Content>
                </gauge:ContentPointer>
            </gauge:RadialAxis.Pointers>
        </gauge:RadialAxis>
    </gauge:SfRadialGauge.Axes>
</gauge:SfRadialGauge>

{% endhighlight %}

{% highlight c# %}

SfRadialGauge sfRadialGauge = new SfRadialGauge();

RadialAxis radialAxis = new RadialAxis();
sfRadialGauge.Axes.Add(radialAxis);

ContentPointer contentPointer = new ContentPointer();
contentPointer.Value = 60;
contentPointer.MarkerOffset = -0.1;
contentPointer.OffsetUnit = SizeUnit.Factor;
contentPointer.IsInteractive = true;
Grid contentPointerRootChild = new Grid
{
    Background = new SolidColorBrush(Colors.Orange),
    BorderBrush = new SolidColorBrush(Colors.Black),
    BorderThickness = new Thickness { Bottom = 1, Left = 1, Right = 1, Top = 1 },
    CornerRadius = new CornerRadius { BottomLeft = 4, BottomRight = 4, TopLeft = 4, TopRight = 4 }
};
contentPointerRootChild.Children.Add(new TextBlock
{
    Text = "60",
    Margin = new Thickness { Bottom = 2, Left = 2, Right = 2, Top = 2 }
});

contentPointer.Content = contentPointerRootChild;
radialAxis.Pointers.Add(contentPointer);

this.Content = sfRadialGauge;

{% endhighlight %}

{% endtabs %}

![WinUI Radial Gauge Marker Offset](images/content-pointer/content-pointer-offset.png)

N> Provide positive value to [`MarkerOffset`](https://help.syncfusion.com/cr/winui/Syncfusion.UI.Xaml.Gauges.MarkerPointer.html#Syncfusion_UI_Xaml_Gauges_MarkerPointer_MarkerOffset) to move the pointer inside of the axis and negative value to move the pointer outside of the axis.
