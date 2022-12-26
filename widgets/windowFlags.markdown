一·功能效果：



二.实现方式
	(一）.ControllerWindow 类：
	
		

	1、QGroupBox的实现方式：利用布局增加内部的互斥按钮。
	QGroupBox *typeGroupBox;
	 typeGroupBox = new QGroupBox(tr("Type"));

	 QRadioButton *windowRadioButton;
	 QRadioButton *dialogRadioButton;
	layout->addWidget(windowRadioButton, 0, 0);
	 typeGroupBox->setLayout(layout);

	2、几个工具函数：创建UI界面的工具。
	void createTypeGroupBox();
	void createHintsGroupBox();
       QCheckBox *createCheckBox(const QString &text);
      QRadioButton *createRadioButton(const QString &text);
	
	3、updatePreview ：更新目前窗口的设置。（windowFlags)
	setWindowFlags() 设置窗体标志
	
	来自 <https://blog.csdn.net/weixin_41349971/article/details/111880064> 
	
	(1)Qt::ToolTip：表示窗口小部件是工具提示。 这在内部用于实现工具提示，没有标题栏和窗口框。
	
      （2）Qt::Popup：表示窗口小部件是弹出式顶级窗口，即它是模态的，但具有适合弹出菜单的窗口系统框架。
	
	
	
三.一些疑惑知识点：

  1、textEdit->setLineWrapMode(QTextEdit::NoWrap);  NoWrap是有什么作用:
