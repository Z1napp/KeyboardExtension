# KeyboardExtension


import UIKit

extension UIView {
    func bindToKeyboard() {
        NotificationCenter.default.addObserver(self, selector: #selector(keyboardWillChange(notif:)), name: UIResponder.keyboardWillChangeFrameNotification, object: nil)
    }
    
    @objc func keyboardWillChange(notif: NSNotification) {
        
        let duration = notif.userInfo![UIResponder.keyboardAnimationDurationUserInfoKey] as! Double
        let curve = notif.userInfo![UIResponder.keyboardAnimationCurveUserInfoKey] as! UInt
        let beginningFrame = (notif.userInfo![UIResponder.keyboardFrameBeginUserInfoKey] as! NSValue).cgRectValue
        let endingFrame = (notif.userInfo![UIResponder.keyboardFrameEndUserInfoKey] as! NSValue).cgRectValue
        let deltaY = endingFrame.origin.y - beginningFrame.origin.y
        
        UIView.animateKeyframes(withDuration: duration,
                                delay: 0,
                                options: UIView.KeyframeAnimationOptions(rawValue: curve),
                                animations: {
                                    self.frame.origin.y += deltaY
        }, completion: nil)
    }
}
