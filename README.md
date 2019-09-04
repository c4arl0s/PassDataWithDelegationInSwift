# Pass Data With Delegation In Swift

PassDataWithDelegationInSwift

# Steps to Delegation

# 1. Create a delegate protocol

``` swift
protocol SecondViewControllerDelegate {
    func didTappedButton(message: String)
}
```


# 2. Create a delegate property

``` swift
var delegate: SecondViewControllerDelegate?
 ```
# 3. Adopt, implement the protocol and set the delegate somewhere. It could be on prepare for segue method in this case.

``` swift
class ViewController: UIViewController, SecondViewControllerDelegate {
    @IBOutlet weak var textViewFromSecondViewController: UITextView!
    
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        // find out why you have to prepare for segue!
        // find ouy why you have to delegate until here
        // oh! remember the example seen into appRewiewController code
        if let destination = segue.destination as? SecondViewController {
            destination.delegate = self
        }
    }
    override func viewDidLoad() {
        super.viewDidLoad()
        
    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
    }
    @IBAction func performSegueButtonTapped(_ sender: Any) {
    performSegue(withIdentifier: "goToSecondViewController", sender: nil)
    }
    func didTappedButton(message: String) {
        print(message)
        let date = Date()
        print("at \(date)", date)
        textViewFromSecondViewController.text.append(message + "\(date)")
        
    }
}
```

# 4. Call the delegate.

``` swift
@IBAction func passDataButtonTapped(_ sender: Any) {
        delegate?.didTappedButton(message: "Sent from SecondViewController to FirstViewController")
    }
```

![Screen Shot 2019-09-03 at 9 08 07 PM](https://user-images.githubusercontent.com/24994818/64220434-0c172780-ce8f-11e9-83ea-c89fc3f754ed.png)

# ViewController.swift

``` swift
@IBAction func passDataButtonTapped(_ sender: Any) {
        delegate?.didTappedButton(message: "Sent from SecondViewController to FirstViewController")
    }
```

# SecondViewController.swift

``` swift
//
//  SecondViewController.swift
//  PassDataWithDelegationInSwift
//
//  Created by Carlos Santiago Cruz on 03/11/18.
//  Copyright © 2018 Carlos Santiago Cruz. All rights reserved.
//

import UIKit

protocol PassDataDelegate {
    func finishPassingData(string: String)
}

class SecondViewController: UIViewController {
    var delegate: PassDataDelegate?
    
    override func viewDidLoad() {
        super.viewDidLoad()

    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
    }
    @IBAction func passDataButtonTapped(_ sender: Any) {
        delegate?.finishPassingData(string: "Send from SecondViewController to FirstViewController")
    }

}
```

![Screen Shot 2019-08-28 at 11 33 59 PM](https://user-images.githubusercontent.com/24994818/63910453-59f1e280-c9ec-11e9-9f61-ffee047abc0e.png)
![Screen Shot 2019-08-28 at 11 34 04 PM](https://user-images.githubusercontent.com/24994818/63910456-5bbba600-c9ec-11e9-8b26-ba890919ca91.png)

