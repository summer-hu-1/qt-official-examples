

一.功能

image.png

二.知识点
1.Qt qOverload函数介绍   来自 <https://blog.csdn.net/xiaolong361/article/details/86552374> 
	作用：用来qt5信号与槽之间传递参数。
	(1)c++14 用法：
		  struct Foo {
		      void overloadedFunction();
		      void overloadedFunction(int, QString);
		  };
		  ... qOverload<>(&Foo::overloadedFunction)
		  ... qOverload<int, QString>(&Foo::overloadedFunction)
		备注：其中的模板参数是重载函数参数类型的列表（list）。functionPointer是重载函数（成员函数）的指针。
		
	(2)c++11用法：
	[signal] void QComboBox::currentIndexChanged(int index)
	connect(comboBox, QOverload<int>::of(&QComboBox::currentIndexChanged), this, [=](int index){ /* ... */ });
	
	（3）补充；如果其中有成员函数是const-overloaded类型的，则必须使qConstOverload 和qNonConstOverload
	

2.QComboBox设置关联数据
	（1）itemData()   :  取得关联数据
		penStyleComboBox->itemData( penStyleComboBox->currentIndex(), Qt::UserRole).toInt()） //
		第一个参数就决定取那项；第二参数就表示，取出该项的数据，该数据应该如何表示，就由该函数的第二参数来确定了，如  Qt::UserRole 这个参数 就 告知，取出的数据应该是用  用户自定义的类型来表示。
		
		
		
	（2）setItemData() :  设置关联数据
	shape 的combox additem 用的重载的 可以写QVariant 类型的 
	 shapeComboBox->addItem(tr("Polygon"), RenderArea::Polygon);  //这里是枚举
	  brushStyleComboBox->addItem(tr("Dense 1"), static_cast<int>(Qt::Dense1Pattern));  //这里是重载为int
	
3.tr("&") 和 setBuddy（） 干啥的 ？
	   shapeLabel = new QLabel(tr("&Shape:"));
	  shapeLabel->setBuddy(shapeComboBox);  //伙伴（buddy）就是就是一个窗口部件
	解答：也就是 ALT + S 就把焦点 跳到shapeLabel的伙伴 shapeComboBox 上面。


4.Qt USerRole
	void QComboBox::setItemData ( int index, const QVariant & value, int role = Qt::UserRole );
	bool QStandardItemModel::setData ( const QModelIndex & index, const QVariant & value, int role = Qt::EditRole );
	
	Qt::UserRole相当于一个索引的作用，一个索引对应一个数据类型的作用。
	
https://www.cnblogs.com/kongbursi-2292702937/p/15007105.html

三.相关链接
	
	1详解官方示例：. <https://blog.csdn.net/weixin_42837024/article/details/105227485> 
	
	
