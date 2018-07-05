# UIPickerView Configuration
Step by Step to Config UIPickerView on your ViewController -  SWIFT

#### Step 01

Initialize UIPickerView on your ViewController.

```
  let statusPicker = UIPickerView()

```

#### Step 02

Add Picker list in to your ViewController

```
  let statusList : [String] = ["Pending","Approved","Rejected"]

```

#### Step 03

Connect UIPickerView Delegate and DataSource 

```
    func configPicker() {
        self.status.inputView = self.statusPicker
        self.statusPicker.delegate = self
        self.statusPicker.dataSource = self
        self.statusPicker.autoresizingMask = [.flexibleWidth,.flexibleHeight]
    }

```

#### Step 04

Add ``inputAccessoryView`` to the TextField.

```
func addToolBar() {
        let toolbarStatus = UIToolbar()
        toolbarStatus.sizeToFit()
        
        let doneStatusButton = UIBarButtonItem(barButtonSystemItem: .done, target: nil, action: #selector(doneSelect))
        let spaceButton3 = UIBarButtonItem(barButtonSystemItem: UIBarButtonSystemItem.flexibleSpace, target: nil, action: nil)
        toolbarStatus.setItems([spaceButton3, doneStatusButton], animated: false)
        
        self.status.inputAccessoryView = toolbarStatus
    }

```

#### Step 05

Add Selector for Done Button.

```
  @objc func doneDateSelect() {
        self.view.endEditing(true)
   }

```

#### Step 06

Add ``UIPickerViewDataSource`` and ``UIPickerViewDelegate``

```
    extension YourViewController: UIPickerViewDataSource {
    
      func numberOfComponents(in pickerView: UIPickerView) -> Int {
          return 1
      }
    
      func pickerView(_ pickerView: UIPickerView, numberOfRowsInComponent component: Int) -> Int {
          if pickerView == self.statusPicker {
              return self.statusList.count
          } else {
              return 0
          }
      }
    
      func pickerView(_ pickerView: UIPickerView, titleForRow row: Int, forComponent component: Int) -> String? {
          if pickerView == self.statusPicker {
              return self.statusList[row]
          } else {
              return nil
          }
      }
    
  }

  extension YourViewController: UIPickerViewDelegate {
    
      func pickerView(_ pickerView: UIPickerView, didSelectRow row: Int, inComponent component: Int) {
          if pickerView == self.statusPicker {
              self.status.text! = self.statusList[row]
          }
      }
    
  }



```

#### Step 07

Add ``addToolBar()`` and ``configPicker()`` to ``viewDidLoad()``

```
  override func viewDidLoad() {
        super.viewDidLoad()
        self.addToolBar()
        self.configPicker()
   }

```


