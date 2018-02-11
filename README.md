# 页面结构
  所有app所有功能页面分为两个部分，一个部分为页面的头部xxxx，另一个部分为页面的内容xxxx_frame，使用apicloud打开的头部为win，内容页为frame
# 页面打开逻辑

  main页面功能：
  在apicloud里面创建项目，然后使用apicloud Studio登录下载到本地，index打开main（win），main打开main_frame和minicart_frame，基本上
  都是看点击的功能，先打开xxxx，再在xxxx中打开它所属的内容页xxxx_frame
# 功能实现逻辑
  1.首先通过aMap地图模块获取当前的位置信息，判断当前地理位置和页面显示城市是否一致，不一致就打开城市选择页面cityselector_frame，在cityselector_frame页面中，通过api.ajax获取后台数据显示在页面中，给每条数据绑定一个点击事件，传个i作为每条数据的标识符，然后在点击事件中通过api.setStorage()保存到本地，再设置一个自定义事件把当前点击的城市广播出去，供main页面接收
  2.在main页面刚进来的时候先通过api.getStorage()判断是否存在当前城市，不存在就打开城市选择页面cityselector_frame，存在的话就调用更新页面中的城市名称的方法
  3.在main页面设置监听事件addEventListener（）获取城市选择页面cityselector_fram选择页面的自定义事件，获取到城市就调用更新页面城市名称的方法和打开首页所有需要打开的frame的方法
  4.设置打开需要打开的frame的方法：用到api.openFrameGroup（）方法，把5个分类（水果，蔬菜，零食，食材，牛奶）放在group里面（具体实现方法看apicloud文档），在成功回调中更新设置选择菜单状态的方法；用api.openFrame()方法打开mini购物车，并通过api.bringFrameToFront设置购物车放在所有frame的最前面
  5.设置首页main_frame打开个人中心标签的方法，首先$api.getStorage获取本地缓存中的用户数据（这个数据由login_frame页面中通过api.setStorage()保存），如果存在数据就直接打开个人中心personalcenter，如果不存在的话就打开login登录页面。
  
  login页面功能：
  1.定义全局变量存放用户名和密码。获取登录页面输入的用户名和密码，通过ajax发送到后台，成功后通过api.setStrorage()保存到本地中，这个发送到ajax的用户名可以是登录页面输入的，也可以是是注册页面传送过来的，
  
  register页面功能
  1.获取注册页面输入的用户名和密码，，通过ajax发送到后台，成功后通过api.alert提示，在这个方法的回调中通过api.execScript跨页面方法吧注册的用户名传到登录页面的fnSetUsername（）方法中
  
  personalcenter页面
  1.
