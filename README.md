# LabelDemo-swift
swift-label各种属性

        //1.创建
        let label=UILabel(frame:CGRect(origin: CGPoint(x:100,y:100),size: CGSize(width:200,height:100)))
        
        //label.frame = CGRect(origin: CGPoint(x:100,y:100),size: CGSize(width:200,height:40))
        label.backgroundColor=UIColor.green
        
        //2、设置和读取文本内容，默认为nil
        label.text = "1234545874573852345343"
        
        // 3、设置文字颜色，默认为黑色
        label.textColor = UIColor.red
        
        // 4、font设置文字大小，默认为17
        label.font=UIFont.systemFont(ofSize: 20)//一般方法
        label.font=UIFont.boldSystemFont(ofSize: 20)//加粗方法
        label.font=UIFont.init(name:"Avenir-Oblique", size: 20)////指定字体的方法
        
        // 5、textAlignment设置标签文本对齐方式
        label.textAlignment = NSTextAlignment.center
        
        // 6、numberOfLines标签最多显示行数，如果为0则表示多行
        label.numberOfLines = 2
        
        // 7、enabled只是决定了Label的绘制方式，将它设置为NO时文本变暗，表示没有激活，这是向她设置颜色值都是无效的。
        //label.isEnabled = false
        
        // 8、highlighted是否高亮显示
        label.isHighlighted = true
        label.highlightedTextColor=UIColor.yellow//高亮显示时候的文本颜色
       
        // 9、ShadowColor设置阴影颜色
        label.shadowColor=UIColor.blue
        
        // 10、ShadowOffset设置阴影偏移量
        label.shadowOffset = CGSize(width: -1, height: 1)
        
        // 11、baselineAdjustment如果==YES，控制文本基线的行为
        /*
         UIBaselineAdjustmentAlignBaselines = 0, // default. used when shrinking text to position based on the original baseline默认，文本最上端与中线对齐。
         UIBaselineAdjustmentAlignCenters, //文本中线与label中线对齐。
         UIBaselineAdjustmentNone, //文本最低端与label中线对齐。
         */
        label.baselineAdjustment = UIBaselineAdjustment.none
        
        // 12、Autoshrink是否自动收缩
        /*
         Fixed Font Size默认，如果label宽度小于文字长度时，文字大小不自动缩放
         minimumScaleFactor设置最小收缩比例，如果Label宽度小于文字长度时，文字进行收缩，收缩超过比例后，停止收缩。
        */
        label.minimumScaleFactor = 0.5
        label.adjustsFontSizeToFitWidth = true// 13、adjustsLetterSpacingToFitWidth改变字母之间的间距来适应Label大小
        
        // 14、lineBreakMode设置文字过长时的显示格式
        //label.lineBreakMode = NSLineBreakMode.byCharWrapping//以字符为显示单位显示，后面部分省略不显示
        //        label.lineBreakMode=NSLineBreakMode.byClipping//剪切与文本宽度相同的内容长度，后半部分被删除。
        //        label.lineBreakMode=NSLineBreakMode.byTruncatingHead//前面部分文字以……方式省略，显示尾部文字内容。
        //        label.lineBreakMode=NSLineBreakMode.byTruncatingMiddle//中间的内容以……方式省略，显示头尾的文字内容。
        //        label.lineBreakMode=NSLineBreakMode.byTruncatingTail//结尾部分的内容以……方式省略，显示头的文字内容。
        //        label.lineBreakMode=NSLineBreakMode.byWordWrapping//以单词为显示单位显示，后面部分省略不显示。
        
        // 16、attributedText设置标签属性文本    
        let text:NSString = "will.JJ"
        let textLabelStr = NSMutableAttributedString.init(string: text as String)
        let bodyFont = [NSFontAttributeName:UIFont.preferredFont(forTextStyle: UIFontTextStyle.body)]
        textLabelStr.setAttributes(bodyFont, range: NSMakeRange(2, 5))
        label.attributedText = textLabelStr;
        
        // 17、竖排文字显示每个文字加一个换行符，这是最方便和简单的实现方式。
        //        label.text="这\n个\n是\n竖\n排\n方\n向\n的\n显\n示"
        //        label.numberOfLines=0
        
        // 18、计算UILabel随字体多行后的高度
        let bounds:CGRect=CGRect(origin: CGPoint(x:100,y:100),size: CGSize(width:200,height:100))
        let heightLabel:CGRect = label.textRect(forBounds: bounds, limitedToNumberOfLines:1)//计算20行之后的Label的Frame
        print("%f",heightLabel.size.height)
        
        // 19、UILabel根据字数多少自动实现适应高度
        let msgLabel=UILabel(frame:CGRect(origin: CGPoint(x:100,y:300),size: CGSize(width:200,height:100)))
        msgLabel.text = "用于管理内容的绘制有关的对象显示在一个滚动视图应该瓦片的内容的子视图，以便没有视图超过屏幕的大小。当用户在滚动滚动视图，这个对象应该添加和删除子视图是必要的。"
        //创建NSMutableAttributedString
     //        let attributesString = NSMutableAttributedString.init(string: label.text!)
     //        //创建NSMutableParagraphStyle
     //        let paraghStyle = NSMutableParagraphStyle()
     //        //设置行距(同样着这里可以设置行号,间距,对其方式)
     //        paraghStyle.lineSpacing = 10
     //        //添加属性,设置行间距
     //        attributesString.addAttributes([NSParagraphStyleAttributeName : paraghStyle], range: NSMakeRange(0, (label.text?.characters.count)!))
     //        label.attributedText = attributesString
             msgLabel.font = UIFont.systemFont(ofSize: 14
             )
             msgLabel.textColor = UIColor.red
             let string:NSString = msgLabel.text! as NSString
             let options:NSStringDrawingOptions = .usesLineFragmentOrigin
             let boundingRect = string.boundingRect(with: CGSize(width: 200,height: 0), options: options, attributes:[NSFontAttributeName:msgLabel.font], context: nil)
             msgLabel.frame = CGRect(origin: CGPoint(x:100,y:230),size: CGSize(width:200,height:boundingRect.height))
             msgLabel.numberOfLines = 0;
             msgLabel.lineBreakMode = NSLineBreakMode.byWordWrapping
             self.view.addSubview(msgLabel)

             // 20、渐变字体Label
             //let img:UIImage = UIImage.init(named: "btn.png")!
             //let titleColor:UIColor = UIColor.init(patternImage: img)
             let titleColor:UIColor=UIColor.init(patternImage:UIImage.init(named:"btn.png")!)
             let title:NSString="Setting"
             let titleLabel:UILabel=UILabel.init(frame: CGRect(origin: CGPoint(x:100,y:400),size: CGSize(width:80,height:44)))
             titleLabel.textColor = titleColor
             titleLabel.text = title as String
             titleLabel.font=UIFont.boldSystemFont(ofSize: 20)
             titleLabel.backgroundColor=UIColor.clear
             self.view.addSubview(titleLabel)

             // 21、Label添加边框
             titleLabel.layer.borderColor=UIColor.gray.cgColor
             titleLabel.layer.borderWidth=2

             // 22、设置圆角
             titleLabel.layer.cornerRadius=10
             titleLabel.backgroundColor=UIColor.cyan

             // 23、设置背景色圆角
             titleLabel.clipsToBounds = true
             view.addSubview(label)
        
![](https://github.com/jixiang0903/LabelDemo-swift/blob/master/WechatIMG48.jpeg)  
