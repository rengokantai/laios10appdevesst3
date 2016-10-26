# laios10appdevesst3
##1. Other UI Controls
###1 Picker views
####00:33 Picker view
add pins -> s o cmd =

####01:30
b6(connection inspector)-> datasource->ctrl click ->drag to controller


####03:05
```
class ViewController:UIViewController,UIPickerViewDataSource, UIPickerViewDelegate
let items:[String]=['a','b']
```
impl two functions:
```
func numberOfComponents(in pickerView:UIPickerView)->Int{
  return 1
}
```

```
func pickerView(_ pickerView:UIPickerView,numberOfRowsInComponent component:Int)->Int{
  return items.count
}
```
####06:07
remember, the data source just defines the number of rows and columns.  
The delegate defines what's going to be inside of those rows and columns.  

```
func pickerView(_ pickerView:UIpickerView,titleForRow row:int,forComponent component:int)->String?{
  return items[row]
}
```
###2 Picker views with multiple components
####01:00multiple components
2-d array
```
let items:[[String]]=[['a','b'],['c','d']]
```

```
func numberOfComponents(in pickerView:UIPickerView)->Int{
  return items.count
}
```

```
func pickerView(_ pickerView:UIPickerView,numberOfRowsInComponent component:Int)->Int{
  return items[component].count
}
```

```
func pickerView(_ pickerView:UIpickerView,titleForRow row:int,forComponent component:int)->String?{
  return items[component][row]
}
```
###3 Respond to a selection in a picker view
####00:35
opt click file->open assistant editor (it bug arises, product->clean)

####02:21 listen click row event  
```
func pickerView(_ pickerView:UIPickerView, didSelectRow row:Int,inComponent component:Int){
  label.text=items[component][row]
}
```


###4 Create UI elements with code
####02:00
```
let label:UILabel = UILabel(frame:CGRect(x:20,y:20,width:100,height:100))
labe.text=""
view.addSubview(label)

let button:UIButton = UIButton(frame:CGRect(x:20,y:20,width:100,height:100))
button.setTitle("",for:.normal)
button.backgroundColor=UIColor.darkGray
button.addTarget(self,action:#selector(didClick),for .touchUpInside)

func didClick(){print("test")}

//func didClick(btn:UIButton){btn.setTitle("new",for:.normal)}

```

###5 Alert controller popup messages
Four steps
- Step one is to create an alert controller.The alert controller is the manager, or you can think of it as the whole unit, that whole alert or whole pop up that we see. 
- Then we need to create an alert action. Actions are the buttons with the connected responses, when that button is tapped. 
- Then you need to connect the controller to the action. 
- And finally, you need to present the alert. 

```
@IBAction func showAlert(){
  let alert:UIAlertController = UIAlertController(title: "Title", message:"",preferredStyle: .alert)
  let action1:UIAlertAction = UIAlertAction(title:"Cancel",style:.cancel){(_:UIAlertAction) in  print("cancelled")
  alert.addAction(adtion1)
  self.present(alert,animated:true){
    print("completed")
  }
}
```
###6 Sliders and progress bars
####03:32
add event for slider:  
Connection:Action  
Name(any): didMoveSlider  
Type:UISlider  
Event: Value Changed

####04:27
```
IBOutlet weak var progBar:UIProgressView
@IBAction func didMoveSlider(_ sender:UISlider){
  progBar.progress = sender.value    
}
```

####06:22
```
let percent:Float = sender.value/sender.maximunValue
```

###7 Switches and activity indicators
####03:56 add action to switch
COnnection:action
Type: UISwitch  
Event:Value Changed  
Arguments: Sender

```
@IBOutlet weak var myIndicator:UIActivityIndicatorView!
@IBAction func switchDidChange(_ sender:UISwitch){}
```


















##2. Web Views
###1 Web views
UIWebView is deprecated, use WKWebView  

####02:15
ViewController.swift
```
import WebKit

class ViewController:UIViewController{
  var webView:WKWebView!
  
  override func viewDidLoad(){
  super.viewDisLoad()
  webView = WKWebView(from: CGRect(x:0,y:20,width:300,height:300)
  view.addSubview(webView)
  //test
 //params: webView.loadHTMLString(string:String,baseURL:URL?)
 webView.loadHTMLString("<p>test</p>",baseURL:nil)
  }
  
}
```

###2 Load a file into a web view
[old version](http://stackoverflow.com/questions/28748650/nsbundle-mainbundle-urlforresourcebach1-withextension-jpg-returning-nu)
3.0 vs old:
```
//swift 3.0
if let resourceUrl = Bundle.main.url(forResource: "test", withExtension: "jpg") {
    if FileManager.default.fileExists(atPath: resourceUrl.path) {
        print("file found")
    }
}
```
```
//old
if let resourceUrl = NSBundle.mainBundle().URLForResource("test", withExtension: "jpg") {
    if NSFileManager.defaultManager().fileExistsAtPath(resourceUrl.path!) {
        print("file found")
    }
}
```

Hence
```
let url:URL = BBundle.main.url(forResource:"page",withExtension:"html")! //swift3.0
let req:URLRequest = URLRequest(url:url)
webView.load(req)
```
###3 Load a URL into a web view
```
let url:URL=URL(string:"http://www.google.com")!
let req:URLRequest=URLRequest(url:url)
webView.load(req)
```

###4 Create layout constraints with code
ViewController.swift
```
override func viewDisLoad(){
  super.viewDidLoad()
  webView = WKWebView()
  view.addSubView(webView)
  ...
  webView.translatesAutoresizingMaskIntoConstraints = false
  let width =NSLayoutConstraint(item:webView,attribute:.width, relatedBy:.equal,toItemLview,attribute:.width,multiplier:1.0,constant:0)
  let height =NSLayoutConstraint(item:webView,attribute:.height, relatedBy:.equal,toItemLview,attribute:.height,multiplier:1.0,constant:0)
  view.addConstraints([width,height])
}
```



















##3. Size Classes
###1 Basics of size classes
####01:36  
iphone SE portrait:
w->C(compact)  
h->R(regular)  
iphone SElandscape:
w->C(compact)  
h->C(compact)  
iphone 6 plus portrait:
w->R(regular) 
h->C(compact)  
h->R(regular)  

####03:48 introduce variations based on
####04:40
You can add extra components. When completed, click `done varying`

###2 Font sizes with size classes
####02:20
the only phone in landscape modewith regular(R) width is plus level (6+)


###3 Pins with size classes
####01:40 add pins
####02:16 resolve auto layout issues
update frames

####02:56
What if I wanted to maintain the same size squares here? So, let's say, when we lay it out in landscape, we don't wanna squish these squares, we want them to be next to each other.  

####03:20
(landscape mode)->vary for traits->check height  
delete all pins:  
size inspector->delete all pins

####05:26
rotate screen in simulator:cmd ->








