# WPF深入浅出

## 命令
- 1.1 命令的基本元素与关系

```shell script
命令:Command
命令源:Command Source
命令目标:Command Target
命令关联:Command Binding
```
## 资源
```shell script
动态资源程序运行过程中可能改变的资源:StacicResource
静态资源程序运行过程中不再改变的资源:DynamicResource
资源路径:
pack:application,,,[/程序集名;][可选版本号;][文件夹名;/]文件名
```
## 模板
形而上者为之到，形而下者为之器
```shell script
Template
DataTemplate
ControllTemplate
```
- 1.1 DataTemplate数据的外衣
    - ContentControl的ContentTemplate    
    - ItemControl的ItemTemplate    
    - GridViewControl的GridViewTemplate
    
- 1.2 ControlTemplate，控件的外衣
    - 通过更换ControlTemplate改变控件的外观
    - 借助ControlTemplate，设计师，程序员可以并行工作

- 1.3 PanelTemplate

## Style
- 1.1 Setter

- 1.2 Trigger
- 1.3 DataTrigger
- 1.4 MultiTrigger
- 1.4 EventTrigger
``` html script
 <Style x:Key="default" TargetType="{x:Type Button}">
                <Setter Property="Foreground" Value="black"/>
                <Setter Property="Width" Value="150"/>
                <Setter Property="Height" Value="50"/>
                <Setter Property="Template">
                    <Setter.Value>
                        <ControlTemplate>
                            <StackPanel Orientation="Horizontal" Margin="2">
                                <Image Source="/img/play.png" Stretch="Uniform" Opacity="0.8"/>
                                <TextBlock Text="default" Style="{DynamicResource defaultTxt}"/>
                            </StackPanel>
                        </ControlTemplate>
                    </Setter.Value>
                </Setter>
            <Style.Triggers>
                <Trigger Property="IsEnabled" Value="false">
                    <Setter Property="Opacity" Value="0.23"/>
                </Trigger>
                <EventTrigger RoutedEvent="Mouse.MouseEnter">
                    <EventTrigger.Actions>
                        <BeginStoryboard>
                            <Storyboard>
                                <DoubleAnimation Duration="0:0:0.5"  Storyboard.TargetProperty="(Button.Width)"  To="200"></DoubleAnimation>
                            </Storyboard>
                        </BeginStoryboard>
                    </EventTrigger.Actions>
                </EventTrigger>
                <EventTrigger RoutedEvent="Mouse.MouseLeave">
                    <EventTrigger.Actions>
                        <BeginStoryboard>
                            <Storyboard>
                                <DoubleAnimation Duration="0:0:0.5"  Storyboard.TargetProperty="(Button.Width)"  ></DoubleAnimation>
                            </Storyboard>
                        </BeginStoryboard>
                    </EventTrigger.Actions>
                </EventTrigger>
            </Style.Triggers>
            </Style>
```

