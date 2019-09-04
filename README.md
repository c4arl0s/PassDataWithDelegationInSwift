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
//
//  ViewController.swift
//  PassDataWithDelegationInSwift
//
//  Created by Carlos Santiago Cruz on 03/11/18.
//  Copyright © 2018 Carlos Santiago Cruz. All rights reserved.
//

import UIKit

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

protocol SecondViewControllerDelegate {
    func didTappedButton(message: String)
}

class SecondViewController: UIViewController {
    var delegate: SecondViewControllerDelegate?
    
    override func viewDidLoad() {
        super.viewDidLoad()

    }

    override func didReceiveMemoryWarning() {
        super.didReceiveMemoryWarning()
    }
    @IBAction func passDataButtonTapped(_ sender: Any) {
        delegate?.didTappedButton(message: "Sent from SecondViewController to FirstViewController")
    }

}
```

![Screen Shot 2019-09-03 at 9 35 34 PM](https://user-images.githubusercontent.com/24994818/64221528-cfe5c600-ce92-11e9-9b87-d91ede041904.png)
![Screen Shot 2019-09-03 at 9 35 40 PM](https://user-images.githubusercontent.com/24994818/64221531-d116f300-ce92-11e9-91d9-25a35295a78c.png)
![Screen Shot 2019-09-03 at 9 35 43 PM](https://user-images.githubusercontent.com/24994818/64221538-d3794d00-ce92-11e9-9757-eea5dc8d0706.png)
