# UIKit

## UICollectionView

### Dynamic self-sizing `UICollectionViewCell`

```swift
class CustomCell : UICollectionViewCell {
  override func preferredLayoutAttributesFitting(_ layoutAttributes: UICollectionViewLayoutAttributes) -> UICollectionViewLayoutAttributes {
    self.setNeedsLayout()
    self.layoutIfNeeded()

    let size = contentView.systemLayoutSizeFitting(layoutAttributes.size)
    var frame = layoutAttributes.frame
    frame.size.height = ceil(size.height)
    layoutAttributes.frame = frame
    return layoutAttributes
  }
}

class ViewController : UIViewController, UICollectionViewDelegate, UICollectionViewDataSource {
  @IBOutlet weak var collectionView: UICollectionView!
	
  override func viewDidLoad() {
    super.viewDidLoad()
    // ** set data **
		
    DispatchQueue.main.async {
      if let flowLayout = self.collectionView.collectionViewLayout as? UICollectionViewFlowLayout,
        let collectionView = self.collectionView {
        let w = collectionView.frame.width
        flowLayout.estimatedItemSize = CGSize(width: w, height: 20)
      }
    }
  }
}
```
