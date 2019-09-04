# Pass Data With Delegation In Swift

PassDataWithDelegationInSwift

# Steps to Delegation

1. Create a delegate protocol

``` swift
protocol PassDataDelegate {
    func finishPassingData(string: String)
}
```


2. Create a delegate property

``` swift
 var delegate: PassDataDelegate?
 ```
3. Adopt and implement the protocol.
4. Call the delegate.

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

class ViewController: UIViewController, PassDataDelegate {
    
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        // find out why you have to prepare for segue!
        if let destination = segue.destination as? SecondViewController {
        // find ouy why you have to delegate until here
        // oh! remember the example seen into appRewiewController code
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
    func finishPassingData(string: String) {
        print(string);
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

# New Changes

``` swift
//
//  ViewController.swift
//  PassDataWithDelegationInSwift
//
//  Created by Carlos Santiago Cruz on 03/11/18.
//  Copyright © 2018 Carlos Santiago Cruz. All rights reserved.
//

import UIKit

class ViewController: UIViewController, PassDataDelegate {
    @IBOutlet weak var textViewFromSecondViewController: UITextView!
    
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        // find out why you have to prepare for segue!
        if let destination = segue.destination as? SecondViewController {
        // find ouy why you have to delegate until here
        // oh! remember the example seen into appRewiewController code
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
    func finishPassingData(string: String) {
        print(string);
        //textViewFromSecondViewController.text = textViewFromSecondViewController.text + string
        let date = Date()
        print("at \(date)", date)
        textViewFromSecondViewController.text.append(string + "\(date)")
        
    }
}
```

![Screen Shot 2019-09-01 at 5 27 07 PM](https://user-images.githubusercontent.com/24994818/64083238-f87a8e00-cce1-11e9-8aba-ff63093eee13.png)
