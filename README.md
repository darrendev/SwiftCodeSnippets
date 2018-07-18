# SwiftCodeSnippets

# Swift Code Snippets

**Note:** `cs` is short for `Code Snippets`

## 1. Protocols

##### 1.1 csComparable

``` swift
extension <#type#>: Comparable {
    static func < (lhs: <#type#>, rhs: <#type#>) -> Bool {
        return lhs.<#property#> < rhs.<#property#>
    }
}
```

##### 1.2 csEquatable

``` swift
extension <#type#>: Equatable {
    static func == (lhs: <#type#>, rhs: <#type#>) -> Bool {
        return lhs.<#property#> == rhs.<#property#>
    }
}
```

##### 1.3 csHashable

``` swift
extension <#type#>: Hashable {
    var hashValue: Int {
        return <#hashValue#>
    }
}
```


## 2. SnapKit

##### 2.1 csSnpMake

``` swift
<#view#>.snp.makeConstraints {
    <#code#>
}
```

##### 2.2 csSnpUpdate

``` swift
<#view#>.snp.updateConstraints {
    <#code#>
}
```

##### 2.3 csSnpTop

``` swift
$0.top.equalToSuperview().offset(<#value#>)
```

##### 2.4 csSnpBottom

``` swift
$0.bottom.equalToSuperview().offset(-<#value#>)
```

##### 2.5 csSnpLeft

``` swift
$0.left.equalToSuperview().offset(<#value#>)
```

##### 2.6 csSnpRight

``` swift
$0.right.equalToSuperview().offset(-<#value#>)
```

##### 2.7 csSnpCenter

``` swift
$0.center.equalTo<#view#>()
```

##### 2.8 csSnpCenterX

``` swift
$0.centerX.equalTo<#view#>()
```

##### 2.9 csSnpCenterY

``` swift
$0.centerY.equalTo<#view#>()
```

##### 2.10 csSnpHeight

``` swift
$0.height.equalTo(<#height#>)
```

##### 2.11 csSnpWidth

``` swift
$0.width.equalTo(<#width#>)
```

## 3. Persistence

##### 3.1 csUserDefaults
``` swift
var <#ivar#>: <#type#> {
        get {
            return UserDefaults.standard.bool(forKey: <#userdefaultKey#>)
        }
        set {
            UserDefaults.standard.set(newValue, forKey: <#userdefaultKey#>)
            UserDefaults.standard.synchronize()
        }
    }
```

##### 3.2 csCodableUserDefaults

``` swift
var <#ivar#>: <#codableType#> {
        get {
            let decoder = JSONDecoder()
            if let data = UserDefaults.standard.data(forKey: <#userdefaultKey#>) {
                return try? decoder.decode(<#codableType#>.self, from: data)
            }
            return nil
        }
        set {
            guard let newItems = newValue else { return }
            let encoder = JSONEncoder()
            if let encoded = try? encoder.encode(newItems) {
                UserDefaults.standard.set(encoded, forKey: <#userdefaultKey#>)
            }
        }
    }
```

## 4. Navigation

##### 4.1 csPushVC

``` swift
navigationController?.pushViewController({
            let vc = <#VC#>(viewModel: <#VM#>())
            vc.hidesBottomBarWhenPushed = true
            return vc
        }(), animated: true)
```

## 5. Concurrent

##### 5.1 csGCD

``` swift
DispatchQueue.global().async {
                            
    DispatchQueue.main.async {
                                
    }
}
```

##### 5.2 csGuardSelf

``` swift
guard let `self` = self else { return }
```

## 6. Comments

##### 6.1 csMarkInput

``` swift
// MARK: Input
```

##### 6.2 csMarkOutput

``` swift
// MARK: Output
```

##### 6.3 csMarkTestOnly

``` swift
// MARK: test only
```

##### 6.4 csTodo

``` swift
// TODO: <#todo#>
```

## 7. Patterns

##### 7.1 csSingleton

``` swift
static let shared = <#type#>()
```

## 8. Rx

##### 8.1 csRxBindTableView

``` swift
viewModel.sectionDriver
           .drive( tableView.rx.items(dataSource: RxTableViewSectionedReloadDataSource<<#name#>SectionModel>(configureCell: { [weak self] (dataSource, tableView, indexPath, rowModel) -> UITableViewCell in
                guard let `self` = self else { return UITableViewCell() }
                if let cell = tableView.dequeueReusableCell(withIdentifier: self.cellId, for: indexPath) as? <#name#>Cell {
                  
                    return cell
                } else {
                    return UITableViewCell()
                }
            })))
            .disposed(by: bag)
```

##### 8.2 csRxSetupDatasource

``` swift
import UIKit
import RxSwift
import RxCocoa
import RxDataSources

struct <#name#>RowModel {

}

struct <#name#>SectionModel {
    var items: [Item]
}

extension <#name#>SectionModel: SectionModelType {
    typealias Item = <#name#>RowModel
    init(original: <#name#>SectionModel, items: [Item]) {
        self = original
        self.items = items
    }
}
```
##### 8.3 csSetupVC
``` swift
import UIKit
import RxSwift
import RxCocoa
import RxDataSources
import SnapKit

@objcMembers class <#name#>VC: UIViewController {
    
    private let viewModel: <#name#>ViewModel
    private let bag = DisposeBag()
    
    init(viewModel: <#name#>ViewModel) {
        self.viewModel = viewModel
        
        super.init(nibName: nil, bundle: nil)
    }
    
    required init?(coder aDecoder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        setup()
        bind()
    }
    
    deinit {
        
        
    }
    
}

extension <#name#>VC {
    
    private func setup() {
        automaticallyAdjustsScrollViewInsets = false
        edgesForExtendedLayout = UIRectEdge()
    }
    
    private func bind() {
        
    }
}
```

##### 8.4csSetupVM

``` swift
import UIKit
import RxSwift
import RxCocoa
import RxDataSources

@objcMembers class <#name#>VM: NSObject {

    private let bag = DisposeBag()
    
    override init() {
        super.init()
        setup()
        bind()
    }
    
}

extension <#name#>VM {
    private func setup() {
        
    }
    
    private func bind() {
        
    }
}
```

##### 8.5 csSetupView

``` swift
import UIKit
import RxSwift
import RxCocoa
import RxDataSources
import SnapKit

class <#name#>View: UIView {

    override init(frame: CGRect) {
        super.init(frame: frame)
        setup()
	bind()
    }

    required init?(coder aDecoder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

}

extension <#name#>View {
    
    private func setup() {
        
    }
    
    private func bind() {
        
    }
}
```

##### 8.6 csSetupCell

``` swift
class <#cellName#>: UITableViewCell {
    override init(style: UITableViewCellStyle, reuseIdentifier: String?) {
        super.init(style: style, reuseIdentifier: reuseIdentifier)
        
    }
    
    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
    }
}
```

##### 8.7 csRxCreateObservable

``` swift
private func <#name#>(<#param#>) -> Observable<<#type#>> {
    return Observable<<#type#>>.create { observer in
        
        return Disposables.create()
    }
}
```

##### 8.8 csRxNaviTitle

``` swift
var navigationBarTitleDriver: Driver<String>!
    navigationBarTitleDriver = Driver<String>
        .just(NSLocalizedString("<#title#>", tableName: "", bundle: KDLocalized.bundle(), value: "", comment: ""))
```

##### 8.9 csRxBag

``` swift
private let bag = DisposeBag()
```

##### 8.10 csRxDriveOnNext

``` swift
<#name#>
    .drive(onNext: { [weak self] <#param#> in
        guard let `self` = self else { return }
        
    })
    .disposed(by: bag)
```

##### 8.11 csRxSubscribeOnNext

``` swift
<#name#>
    .subscribe(onNext: { [weak self] <#param#> in
        guard let `self` = self else { return }
        
    })
    .disposed(by: bag)
```

##### 8.12 csRxDriverSubject

``` swift
var <#name#>Driver: Driver<<#type#>> {
    return <#name#>Subject.asDriver(onErrorJustReturn: <#return#>)
}
private var <#name#>Subject = PublishSubject<<#type#>>()
```

##### 8.13 csRxObserverSubject

``` swift
var <#name#>Observer: AnyObserver<<#type#>> {
        return <#name#>Subject.asObserver()
    }
    private var <#name#>Subject = PublishSubject<<#type#>>()
```

##### 8.14 csRxObservableSubject

``` swift
var <#name#>Observable: Observable<<#type#>> {
        return <#name#>Subject.asObservable()
    }
    private var <#name#>Subject = PublishSubject<<#type#>>()
```

## 9. Misc

##### 9.1 csNotiName

``` swift
extension Notification.Name {
    static let <#name#> = Notification.Name("<#name#>")
}
```

##### 9.2 csSetText

``` swift
NSLocalizedString("<#text#>", tableName: "", bundle: KDLocalized.bundle(), value: "", comment: "")
```

##### 9.3 csTick

``` swift
let startTime = NSDate()
```

##### 9.4 csTock

``` swift
print("Time: \(-startTime.timeIntervalSinceNow)")
```

##### 9.5 csSetupWindow

``` swift
window = UIWindow(frame: UIScreen.main.bounds)
window?.backgroundColor = UIColor.white
window?.rootViewController = <#ViewController#>()
window?.makeKeyAndVisible()
```