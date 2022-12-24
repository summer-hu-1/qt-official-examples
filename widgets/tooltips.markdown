一.功能效果
     



二.实现方式
	（一）.SortingBox :  
	class SortingBox : public QWidget
	{
	    Q_OBJECT
	
	public:
	    SortingBox(QWidget *parent = nullptr);    
	
	protected:
	    bool event(QEvent *event) override;
	    void resizeEvent(QResizeEvent *event) override;
	    void paintEvent(QPaintEvent *event) override;
	    void mousePressEvent(QMouseEvent *event) override;
	    void mouseMoveEvent(QMouseEvent *event) override;
	    void mouseReleaseEvent(QMouseEvent *event) override;
	
	private slots:
	    void createNewCircle();
	    void createNewSquare();
	    void createNewTriangle();
	//! [0]
	
	//! [1]
	private:
	    int updateButtonGeometry(QToolButton *button, int x, int y);
	    void createShapeItem(const QPainterPath &path, const QString &toolTip,
	                         const QPoint &pos, const QColor &color);
	    int itemAt(const QPoint &pos);
	    void moveItemTo(const QPoint &pos);
	    QPoint initialItemPosition(const QPainterPath &path);
	    QPoint randomItemPosition();
	    QColor initialItemColor();
	    QColor randomItemColor();
	    QToolButton *createToolButton(const QString &toolTip, const QIcon &icon,
	//! [1]
	                                  const char *member);
	
	//! [2]
	    QVector<ShapeItem> shapeItems;
	    QPainterPath circlePath;
	    QPainterPath squarePath;
	    QPainterPath trianglePath;
	
	    QPoint previousPosition;
	    ShapeItem *itemInMotion;
	
	    QToolButton *newCircleButton;
	    QToolButton *newSquareButton;
	    QToolButton *newTriangleButton;
	};
	
	简介：  (1）构造函数：初始化ToolButtom按钮和创建对应的形状按扭；
			       A: newCircleButton = createToolButton(tr("New Circle"),
				                                       QIcon(":/images/circle.png"),
				                                       SLOT(createNewCircle()));
				B：createShapeItem(circlePath, tr("Circle"), initialItemPosition(circlePath),
				                    initialItemColor());
					
		  （2）六个事件函数 ：event实现函数事件分发的处理效果，显示ToolButtom的提示框信息。
		bool SortingBox::event(QEvent *event)
		{
		//! [5] //! [6]
		    if (event->type() == QEvent::ToolTip) {
		        QHelpEvent *helpEvent = static_cast<QHelpEvent *>(event);
		        int index = itemAt(helpEvent->pos());
		        if (index != -1) {
		            QToolTip::showText(helpEvent->globalPos(), shapeItems[index].toolTip());
		        } else {
		            QToolTip::hideText();
		            event->ignore();
		        }
		
		        return true;
		    }
		    return QWidget::event(event);
		}
		
		  （3）三个信号槽函数：处理新的变化。
		  （4）工具函数：协助处理生成对应的形状块。
		     createShapeItem 、 initialItemPosition、initialItemColor、randomItemPosition、randomItemColor
  （5）几个私有函数：
		
	(二）ShapeItem ： 初始化Item的一些特有属性，没有过多实现，封装作用。
	class ShapeItem
	{
	public:
	    void setPath(const QPainterPath &path);
	    void setToolTip(const QString &toolTip);
	    void setPosition(const QPoint &position);
	    void setColor(const QColor &color);
	
	    QPainterPath path() const;
	    QPoint position() const;
	    QColor color() const;
	    QString toolTip() const;
	
	private:
	    QPainterPath myPath;
	    QPoint myPosition;
	    QColor myColor;
	    QString myToolTip;
	};
	
三.一些疑惑知识点：
 1、 setBackgroundRole(QPalette::Base);

 2 、三角型绘制：获取当前点（相对点），移动起点的上顶角，画底长120，高100的三角形。
  qreal x = trianglePath.currentPosition().x();
    qreal y = trianglePath.currentPosition().y();
    trianglePath.moveTo(x + 120 / 2, y);
    trianglePath.lineTo(0, 100);
    trianglePath.lineTo(120, 100);
    trianglePath.lineTo(x + 120 / 2, y);
	
