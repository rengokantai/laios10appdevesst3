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
