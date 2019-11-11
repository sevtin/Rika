# ksnotification
## 简单易用的通知管理.

###
	```
	/*1、接口实现*/
	class _MyHomePageState extends State<MyHomePage> implements KSObserver {
	  int _counter = 0;
	  static const String increment_counter = 'increment_counter';
	
	  @override
	  void initState() {
	    super.initState();
	    /*2、添加监听*/
	    KSNotificationCenter.shard().addObserver(this, increment_counter);
	  }
	
	  @override
	  void dispose() {
	    /*5、移除监听*/
	    KSNotificationCenter.shard().removeObserver(this, increment_counter);
	    super.dispose();
	  }
	
	  /*4、接收监听消息*/
	  @override
	  receiveNotify(Map message, String name) {
	    if (name == increment_counter){
	      int value = message['num'] as int;
	      setState(() {
	        _counter += value;
	      });
	    }
	  }
	
	  void _incrementCounter() {
	    /*4、发送通知广播*/
	    KSNotificationCenter.shard().post({'num':100}, increment_counter);
	  }
	
	  @override
	  Widget build(BuildContext context) {
	    return Scaffold(
	      appBar: AppBar(
	        title: Text(widget.title),
	      ),
	      body: Center(
	        child: Column(
	          mainAxisAlignment: MainAxisAlignment.center,
	          children: <Widget>[
	            Text(
	              'You have pushed the button this many times:',
	            ),
	            Text(
	              '$_counter',
	              style: Theme.of(context).textTheme.display1,
	            ),
	          ],
	        ),
	      ),
	      floatingActionButton: FloatingActionButton(
	        onPressed: _incrementCounter,
	        tooltip: 'Increment',
	        child: Icon(Icons.add),
	      ), // This trailing comma makes auto-formatting nicer for build methods.
	    );
	  }
	}
	```
