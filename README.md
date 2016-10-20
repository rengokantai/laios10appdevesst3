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
