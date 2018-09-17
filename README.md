# react-native-back

react-natvie的路由中，目前用的比较多的是react-navigation,然而，这个框架没有提供对android物理返回键的支持。
在实际的项目中，出现了这些需求：
1、需要指定返回到某个页面,当然肯定是需要通过页面的名称来判断的。
2、需要判断某个页面是否存在，如果存在则返回到这个页面，如果不存在，则push到这个页面
3、需要在某个页面返回的时候展示一个确认对话框，用户点击了确认才能做返回动作
4、用户点击了android的物理返回键，要求功能与点击了页面的返回按钮功能相同。

这些功能都是使用十分频繁的，然而在react-navigation中居然没有提供对应的方法，这个库为此而产生。

# Feature

提供<Back>组件，功能要求：
1、适配android的物理返回键，不能相互冲突

例如：


MyComp:

```
class MyComp extends Component{
    render(){
        return (
            <Back>
            </Back>
        );
    }
}
```

```
<Back>
    <MyComp>

    </MyComp>
</Back>
```
如果采用嵌套的模式，只响应里面的back,这样就能支持比如某个页面弹出了一个对话框，然后按android的物理返回键取消掉这个对话框。

2、使用简单，只需要包含一下整个页面组件就行
```
<Back target="要返回的页面" pushWhenNotExists={true} confirm="确定要xx吗?" renderButton={_renderButton}>
    <MyComp />
</Back>
```
启动提供四个参数target/pushWhenNotExists/confirm/renderButton,都是可选的

3、不需要redux支持，仅仅依赖react-navigation