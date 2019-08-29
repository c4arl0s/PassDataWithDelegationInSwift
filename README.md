# PassDataWithDelegationInSwift

PassDataWithDelegationInSwift

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
        delegate?.finishPassingData(string: "Send from SecondViewController")
    }

}
```



