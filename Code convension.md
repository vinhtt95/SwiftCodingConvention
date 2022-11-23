

# Code convension

# 1. Project guidelines

## 1.1. **File naming (Quy tắc đặt tên trong project)**

### 1.1.1. Class files

Tên của class, struct, enum, protocol được viết giống như UpperCamelCase; còn lại được viết theo kiểu lowerCamelCase.

Các từ viết tắt thường được viết hoa tất cả các chữ trong tiếng anh nên được viết theo kiểu viết hoa hoặc viết thường tất cả các chữ theo quy ước.

***Nên***

```swift
var utf8Bytes: [UTF8.CodeUnit]
var isRepresentableAsASCII = true
var userSMTPServer: SecureSMTPServer
var userID: UserID
```

***Không nên***

```swift
var UTF8Bytes: [UTF8.CodeUnit]
var isRepresentableAsAscii = true
var userSmtpServer: SecureSMTPServer
var userId: UserID
```

Các từ viết tắt khác nên được viết như các từ thông thường.

```swift
var radarDetector: RadarScanner
var enjoysScubaDiving = true
```

Tên của biến, tham số và các kiểu liên quan nên đặt theo vai trò của nó thay vì đặt theo kiểu dữ liệu. Việc đặt tên theo kiểu dữ liệu làm code trở nên không rõ ràng.

***Nên***

```swift
var greeting = "Hello"
protocol ViewController {
    associatedtype ContentView: View
}

class ProductionLine {
    func restock(from supplier: WidgetFactory)
}
```

***Không nên***

```swift
var string = "Hello"
protocol ViewController {
    associatedtype ViewType : View
}

class ProductionLine {
    func restock(from widgetFactory: WidgetFactory)
}
```

Sử dụng tiền tố `lbl` cho biến và tham số dạng `UILabel`, tiền tố `txt` cho `UITextField`, `tv` cho `UITextView`, `btn` cho `UIButton`, `constraint` cho `NSLayoutConstraint` và `vc` cho `UIViewController`.

```swift
let lblTitle: UILabel!
let txtEmail: UITextField!
let btnDone: UIButton!
let constraintHeightOfTableView: NSLayoutConstraint!

let projectDetailVC = ProjectDetailViewController()
```

### 1.1.2. Asset files

- Tất cả tên resoures phần lớn đặt theo convention sau.

`<WHAT>_<WHERE>_<DESCRIPTION>_<SIZE>(@2x|@3x).png`

`<WHAT> Chỉ ra nguồn resouce này đại diện cho cái gì, thường là tên của View Class để giới hạn sự lựa chọn của resoure này.`

`<WHERE> Mô tả nơi resouce này nằm ở đâu trong app. Các resourec sử dụng ở nhiều màn thường đặt là all, còn các phần cụ thể khác sẽ phải chỉ cụ thể vị trị của phần đó`

`<DESCRIPTION> Mô tả thuộc tính của resouce trên màn hình VD : title, subtitle ...`

`<SIZE> (optional) Chỉ rõ kích thước của resoure này, thường dành cho và dimensions VD: 24px, small, big,…`

- Advantages (Ưu điểm)
    - Sắp xếp vị trí resoures theo màn hình
        
        `<Where> đã mô tả nơi resoure này nằm ở màn hình nào.`
        
    - Tổ chức resoures tốt hơn Browser của IDE thường sắp xếp theo thứ tự alphabe, cho nên các resoures sẽ đc sắp theo theo group ứng với (What) là (ViewController, View,… ) và (Where) để biết resoures nằm ở màn nào.
    - Autocomplete hiệu quả hơn
        
        `Các prefix <What> và <Where> giúp việc tìm kiếm trên browser hiệu quả hơn khi chỉ cần nhập keyword các prefix này để thu gọn kết quả danh sách tìm`
        
    - Không còn name conflict Các resoures ở các màn hình khác nhau hoặc dùng từ khóa “all” còn không sẽ có 1 (Where) riêng biệt sẽ giúp tránh khỏi việc conflict name
    - Resouces name clean hơn, tên resources được đặt 1 cách logic sẽ khiến project của chúng ta cũng clean hơn rất nhiều.

### 1.1.3. Language

Sử dụng tiếng Anh Mỹ để phù hợp với Apple’s API

***Nên***

```swift
let color = "red"
```

***Không nên***

```swift
let colour = "red"
```

### 1.1.4. Enumerations

Theo Apple’ API Design Guidelines của Swift 3, sử dụng lowserCamelCase cho giá trị của enum.

```swift
enum Shape {
    case Rectangle
    case Square
    case TightTriangle
    case EquilateralTriangle
}
```

### 1.1.5. Dictionary

Sử dụng under_score cho key của `Dictionary`.

```swift
let dict = [
    "the_first_key": "value",
    "the_second_key": "The second value"
]
```

# 2. Code guildelines

## 2.1. Swift language

### 2.1.1. Correctness

Hãy coi warnings như là errrors. Quy tắc này hình thành rất nhiều quyết định, như là không sử dụng toán tử `++` hoặc `--`, vòng lặp kiểu C hoặc sử dụng string cho selector.

### 2.1.2. Optionals

Khai báo biến và kiểu trả về của function là optional với `?` khi nó có thể là một giá trị `nil`

Sử dụng unwrapped type qua khai báo `!` chỉ khi biến đố sẽ được khởi tạo trước khi được sử dụng, như là các `subview` sẽ được khởi tạo sau khi vào `viewDidload`.

Khi truy cập đến một giá trị optional, nếu giá trị đó chỉ được truy cập đến một lần hoặc có nhiều giá trị optional trong chuỗi thì sử dụng chuỗi option.

```swift
self.textContainer?.textLabel?.setNeedsDisplay()
```

Sử dụng rằng buộc optional khi việc unwrap và xử lý nhiều công việc với nó.

```swift
if let _textContainer = self.textContainer {
    // do many things with textContainer
}
```

Khi đặt tên cho biến và properties dạng optional, tránh việc đặt tên theo kiểu `optionalString` hoặc `maybeView` bởi vì việc nó là optional đã được mô tả trong type của nó.

Với răng buộc optional, thêm vào tên gốc của biến 1 dấu gạch chân `_` khi cảm thấy phù hợp, thay vì sử dụng tên như: `unwrappedView` hoặc `actualLabel`.

***Nên***

```swift
var subview: UIView?
var volume: Double?

// later on...
if let _subview = subview, _volume = volume {
    // do something with unwrapped subview and volume
}
```

***Không nên***

```swift
var optionalSubview: UIView?
var volume: Double?

if let unwrappedSubview = optionalSubview {
    if let realVolume = volume {
        // do something with unwrappedSubview and realVolume
    }
}
```

### 2.1.3. Avoid Using Force-Unwrapping of Optionals

Nếu có một định danh `foo` của kiểu `FooType?` hoặc `FooType!`, hạn chế force-unwrap nếu có thể.

```swift
if let _foo = foo {
    // Use unwrapped `foo` value in here
} else {
    // If appropriate, handle the case where the optional is nil
}
```

Thay vào đó, nếu muốn dùng chuỗi optional của Swift trong một số trường hợp.

```swift
// Call the function if `foo` is not nil. If `foo` is nil, ignore we ever tried to make the call
foo?.callSomethingIfFooIsNotNil()
```

Chú ý: Rằng buộc `if let` của optional sẽ giúp code an toàn hơn. Do force unwrap dễ dẫn đến crash trong quá trình runtime.

### 2.1.4. CGRect Functions

Tránh việc sử dụng trực tiếp `x`, `y`, `width` hay `height` của 1 `CGRect` mà hãy tương tác với nó thông qua các function [CGGeometry](https://developer.apple.com/library/ios/documentation/GraphicsImaging/Reference/CGGeometry/). 

Tất cả các function được mô tả trong tài liệu trên đều lấy input là `CGRect` và sau đó tính toán để trả về kết quả. Từ đó, tránh được việc sử dụng đọc và ghi trực tiếp data trong cấu trúc của `CGRect`.

***Nên***

```swift
let frame = self.view.frame

let x = CGRectGetMinX(frame)
let y = CGRectGetMinY(frame)
let width = CGRectGetWidth(frame)
let height = CGRectGetHeight(frame)
```

***Không nên***

```swift
let frame = self.view.frame

let x = frame.origin.x
let y = frame.origin.y
let width = frame.size.width
let height = frame.size.height
```

### 2.1.5. Functions and menthods

Free functions, cái mà không đi kèm với một class hay type nào, cần hạn chế sử dụng. Khi có thể thì nên dùng method thay vì free fuctions. Việc này sẽ giúp code dễ đọc và dễ tìm hiểu.

Free funtion sẽ phù hợp khi nó không liên quan đến bất kỳ một type hoặc instance nào.

***Nên***

```swift
let sorted = items.mergeSort()  // easily discoverable
rocket.launch()  // clearly acts on the model
```

***Không nên***

```swift
let sorted = mergeSort(items)  // hard to discover
launch(&rocket)
```

***Free Function Exceptions***

```swift
let tuples = zip(a, b)  // feels natural as a free function (symmetry)
let value = max(x,y,z)  // another free function that feels natural
```

### 2.1.6. Access control

Sử dụng access control không đúng sẽ dẫn đến việc gây bối rỗi cho người khác, gán `private` một cách phù hợp để code rõ ràng và có tính đóng gói hơn. Luôn ưu tiên sử dụng `private` khi cố thể. Chỉ có `static`, `@IBAction`, `@IBOutlet` là có thể đứng trước access control.

***Nên***

```swift
class TimeMachine {  
  private dynamic lazy var fluxCapacitor = FluxCapacitor()
}
```

***Không nên***

```swift
class TimeMachine {  
    lazy dynamic private var fluxCapacitor = FluxCapacitor()
}
```

### 2.1.7. Always specify access control explicitly for top-level definitions

Functions, types và variables ở top-level luôn cần được định nghĩa rõ ràng.

```swift
public var whoopsGlobalState: Int
internal struct TheFez {}
private func doTheThings(things: [Thing]) {}
```

*Chú ý*: Thông thường việc định nghĩa internal cho top-level là không phù hợp và cần cân nhắc trước khi thực hiện khai báo này. Bởi vì khai báo mặc định là `internal`, nên sử dụng lại cùng một khai báo access control là không cần thiết.

`IBAction` và IBOutlet nếu có thể thì nên được khai báo `private`

***Nên***

```swift
class MyViewController {
    @IBOutlet private weak var lblTitle: UILabel!

    @IBAction private func didTapDoneButton(sender: AnyObject) {
        // Do something
    }
}
```

***Không nên***

```swift
class MyViewController {
    @IBOutlet weak var lblTitle: UILabel!

    @IBAction func didTapDoneButton(sender: AnyObject) {
        // Do something
    }
}
```

*Chú ý*: tránh việc cho phép các truy cập không mong muốn từ bên ngoài của class.

### 2.1.8. Final

Class nên được khai báo `final` và chỉ được thay đổi để cho phép phân lớp nếu như cần kế thừa. Do đó, có càng nhiều khai báo `final` ở trong class càng tốt.

### 2.1.9. Control Flow

Nên ưu tiên `for-in` của vòng lặp `for` thay vì `white-condition-increment`.

***Nên***

```swift
for _ in 0..<3 {
    print("Hello three times")
}

for (index, person) in attendeeList.enumerate() {
    print("\(person) is at position #\(index)")
}

for index in 0.stride(to: items.count, by: 2) {
    print(index)
}

for index in (0...3).reverse() {
    print(index)
}
```

***Không nên***

```swift
var i = 0
while i < 3 {
    print("Hello three times")
    i += 1
}

var i = 0
while i < attendeeList.count {
    let person = attendeeList[i]
    print("\(person) is at position #\(i)")
    i += 1
}
```

### 2.1.10. Return First

Khi code với các điều kiện, phần lề bên trái luôn được ưu tiên hơn. Vì thế, không nên lồng các điều kiện `if` với nhau. Vẫn sẽ ổn nếu có nhiều câu lệnh return, điều kiện `guard` được sinh ra để làm việc này.

***Nên***

```swift
func computeFFT(context: Context?, inputData: InputData?) throws -> Frequencies {

    guard let context = context else { throw FFTError.noContext }
    guard let inputData = inputData else { throw FFTError.noInputData }

    // use context and input to compute the frequencies

    return frequencies
}
```

***Không nên***

```swift
func computeFFT(context: Context?, inputData: InputData?) throws -> Frequencies {

    if let context = context {
        if let inputData = inputData {
            // use context and input to compute the frequencies

        return frequencies
    }
    else {
        throw FFTError.noInputData
    }
    }
    else {
        throw FFTError.noContext
    }
}
```

Khi có nhiều lệnh unwrap cho các giá trị optional được sử dụng bằng guard hoặc if let, hạn chế việc lồng chúng lại với nhau.

***Nên***

```swift
guard let _number1 = number1, _number2 = number2, _number3 = number3 else { fatalError("impossible") }
    // do something with numbers
```

***Không nên***

```swift
if let _number1 = number1 {
    if let _number2 = number2 {
        if let _number3 = number3 {
            // do something with numbers
        } else {
            fatalError("impossible")
        }
    } else {
        fatalError("impossible")
    }
} else {
    fatalError("impossible")
}
```

### 2.1.11. Implicit Getters

Ưu tiên việc sử dụng implicit getters với các read-only properties và subscripts.

Bỏ từ khóa `get` với read-only properties và subscripts.

***Nên***

```swift
var myGreatProperty: Int {
    return 4
}

subscript(index: Int) -> T {
    return objects[index]
}
```

***Không nên***

```swift
var myGreatProperty: Int {
    get {
        return 4
    }
}

subscript(index: Int) -> T {
    get {
        return objects[index]
    }
}
```

### 2.1.12. Struct Initializers

Sử dụng khởi tạo native của Swift thay vì các legacy constructor của CGGeometry.

***Nên***

```swift
let bounds = CGRect(x: 40, y: 20, width: 120, height: 80)
let centerPoint = CGPoint(x: 96, y: 42)
```

***Không nên***

```swift
let bounds = CGRectMake(40, 20, 120, 80)
let centerPoint = CGPointMake(96, 42)
```

Nên sử dụng `CGRect.infinite`, `CGRect.null`,… thay vì `CGRectInfinite`, `CGRectNull`,…

### 2.1.13. (Optional) Use of self

Để ngắn gọn, Tránh sử dụng `self` bởi vì Swift không cần nó để truy cập đến properties của object hoặc gọi đến các phương thức của object

Sử dụng seft khi cần để phân biệt giữa properties và đối số trong trình khởi tạo, và khi tham chiếu đến các properties trong closure (Theo yêu cầu của compiler).

```swift
class BoardLocation {
    let row: Int, column: Int

    init(row: Int, column: Int) {
        self.row = row
        self.column = column
    }

    let closure = {
        print(self.row)
    }
}
```

## 2.2 Swift style

### 2.2.1. Code Organization

Sử dụng extensions để tổ chức code thành các logical blocks. Mỗi extension nên gán với một

`// MARK: -`

#### 2.2.1.1. Import Statements

import các framework của OS và các framework bên ngoài nên được chia rõ ràng và sắp xếp theo alphabet.

***Nên***

```swift
import Foundation
import UIKit

import Alamofire
import SDWebImage
```

***Không nên***

```swift
import Foundation
import UIKit
import Alamofire
import SDWebImage
```

Phải có đúng một dòng trống giữa giồng import cuối cùng và câu lệnh tiếp theo

#### 2.2.1.2 Protocol Conformance

Khi cho một model tuân thủ theo một `protocol`, ưu tiên việc thêm một `extenstion` để tuân thủ theo `protocol`. Nó giúp cho các methods liên quan được nhóm lại với nhau và đơn hóa việc thêm một `protocol` vào `class` với các menthods liên quan.

***Nên***

```swift
class MyViewController: BaseViewController {
  // class stuff here
}

// MARK: - UITableViewDataSource
extension MyViewController: UITableViewDataSource {
    // table view data source methods
}

// MARK: - UIScrollViewDelegate
extension MyViewController: UIScrollViewDelegate {
    // scroll view delegate methods
}
```

***Không nên***

```swift
class MyViewController: BaseViewController, UITableViewDataSource, UIScrollViewDelegate {
    // all methods
}
```

(Optional) Với view controllers của `UIKit`, nên căn nhắc việc đưa lifecycle, custom accessors, `@IBAction` vào các extension riêng biệt

```swift
class MyViewController: BaseViewController {
    // class stuff here
}

// MARK: - Actions
extension: MyViewController {
    @IBAction func didTapDoneButton(sender: AnyObject) {
        // Handler action
    }
}

// MARK: - APIs
private extension: MyViewController {
    func callAPIToGetUserProfileData() {
    }
}
```

#### 2.2.1.3. Spacing

Thụt lề nên sử dụng 4 dấu cách thay vì tab để tránh bị cắt dòng. Dấu ngoặc nhọn (`if`/`else`/`switch`/`while`/…) luôn được mở ở cùng dòng của câu lệnh nhưng dóng ở một dòng mới.

***Nên***

```swift
if user.isHappy {
    // Do something
} else {
    // Do something else
}
```

***Không nên***

```swift
if user.isHappy
{
  // Do something
}
else {
  // Do something else
}
```

Thêm 1 khoảng trắng ở trước và sau dấu mũi tên return `->` trong functions và closures

***Nên***

```swift
func getLastIndexOfString(string: String) -> Int {
    // ....
}
```

***Không nên***

```swift
func getLastIndexOfString(string: String)->Int {
    // ....
}
```

Nên có 1 dòng trống nằm giữa methods và phần kết thúc của source file để code trở nên rõ ràng và có tổ chức hơn. Khoảng trắng bên trong các methods thường dùng để tách code theo từng vùng chức năng, nhưng nếu có quá nhiều vùng như vậy thì nó cần được chia thành các menthod nhỏ hơn.

```swift
struct MyStruct {
    func functionA() -> Void {
        // Do something
    }

    func functionB() -> String {
        // Do something else
    }
}
```

Dấu hai chấm luôn không có khoảng trắng ở bên trái và có một khoảng trắng ở bên phải. Trừ dấu hai chấm trong ternary operator `? :` và dictionary rỗng `[:]`.

***Nên***

```swift
class TestDatabase: Database {
    var data: [String: CGFloat] = ["A": 1.2, "B": 3.2]
}
```

***Không nên***

```swift
class TestDatabase : Database {
    var data :[String:CGFloat] = ["A" : 1.2, "B":3.2]
}
```

#### 2.2.1.4. Commas

Dấu phẩy `,` không nên có khoảng trắng trước nó, và nên có một khoảng trắng hoặc một dòng mới ở phía sau.

***Nên***

```swift
let array = [1, 2, 3, 4, 5]
let stringArray = ["This", "is", "string", "array"]
let dict = [
    "key": "value",
    "the_second_key": "The second value"
]
```

***Không nên***

```swift
let array = [1,2,3,4,5]
let stringArray = ["This","is","string", "array"]
```

#### 2.2.1.5. Semicolons

Swift không yêu cầu dấu chấm phẩy sau mỗi dòng code. Điều này chỉ được yêu cầu nếu muốn nhóm các dòng code lại thành một dòng.

Không nên gộp nhiều dòng code lại thành một, trường hợp ngoại lệ duy nhất là cho kiến trúc `for-conditional-increment` và nó nên được thay thế bằng kiến trúc `for-in` khi có thể.

***Nên***

```swift
let swift = "not a scripting language"
```

***Không nên***

```swift
let swift = "not a scripting language";
```

#### 2.2.1.6. Braces

Khai báo trống nên được viết trong dấu ngoặc nhọn `{}`

```swift
do {
    let string = try self.getStringFromFileWithPath(path)
} catch {}
```

Nhưng đoạn code trên vẫn chưa đủ để debug mà cần phải in ra lỗi ở trong `catch`.

```swift
do {
    let string = try self.getStringFromFileWithPath(path)
} catch {
    debugPrint(error)
}
```

Đóng ngoặc nhọn `}` không nên có giòng trống trước nó.

***Nên***

```swift
func isRTLLanguage() -> Bool {
    if let isRTL = NSUserDefaults.standardUserDefaults().objectForKey(LCLCurrentLanguageType) as? Bool {

        return isRTL
    }
}
```

***Không nên***

```swift
func isRTLLanguage() -> Bool {
    if let isRTL = NSUserDefaults.standardUserDefaults().objectForKey(LCLCurrentLanguageType) as? Bool {

        return isRTL

    }
}
```

#### 2.2.1.7. Parentheses

Dấu ngoặc đơn sung quanh các lênh điều kiện là không cần thiết và cần được loại bỏ.

***Nên***

```swift
if name == "Hello" && email == "mail@mail.com" {
  print("World")
}
```

***Không nên***

```swift
if (name == "Hello") {
  print("World")
}
```

#### 2.2.1.8. Function Declarations

Không nên sử dụng “and” làm tên tham số truyền vào.

***Nên***

```swift
public func runModalForDirectory(path: String, file name: String, types fileTypes: [String]) -> Int
```

***Không nên***

```swift
public func runModalForDirectory(path: String, andFile name: String, andTypes fileTypes: [String]) -> Int
```

*Chú ý*: mặc dù việc dùng “and” có vẻ hợp lý trong trường hợp này, nhưng nó tạo ra vấn đề khi khai báo methods với nhiều tham số. Nếu như methods mô tả hai hành động tách biệt thì có thể sử dụng “and”.

```swift
func openFile(fullPath: String, withApplication appName: String, andDeactivate flag: Bool) -> Bool
```

#### 2.2.1.9. Return

Nên có một dòng trống trước khi `return`. Trừ trường hợp, functions hoặc closures chỉ có `return`.

```swift
func getUserID() -> Int {
    return self.userID
}

func doSomething() {
    let values = self.getSomeValues()

    return values
}
```

#### 2.2.1.10. Container Literals

Nếu như collection có nhiều hơn một dòng, thêm dấu mở ngoặc trong cùng dòng với dòng khai báo và thêm dấu đóng ngoặc vào một dòng mới và thụt vào lề so với dấu mở ngoặc.

```swift
let stringArray = [
    "This",
    "is",
    "string",
    "array",
]

let dictionary = [
    NSFontAttributeName: UIFont(name: "Helvetica-Bold", size: 12),
    NSForegroundColorAttributeName: UIColor.greenColor()
]
```

### 2.2.2. Code Format

#### 2.2.2.1. (Optional) Type Inference

Ưu tiên các code nhỏ gọn và để trình biên dịch suy ra kiểu cho hằng và biến của instances. Nó phù hợp với các mảng nhỏ (Nhưng không rỗng) và dictionaries. Nên định nghĩa rõ kiểu `CGFloat` hoặc `Int16` khi cần thiết.

***Nên***

```swift
let message = "Click the button"
let currentBounds = computeViewBounds()
var names = ["Mic", "Sam", "Christine"]
let maximumWidth: CGFloat = 106.5
```

***Không nên***

```swift
let message: String = "Click the button"
let currentBounds: CGRect = computeViewBounds()
let names = [String]()
```

#### 2.2.2.2. Ternary Operator

Mục đích của toán tử ba ngôi, ?, là để tăng tính gọn gàng và rõ ràng của code. Nó chỉ nên kiểm tra một điều kiện cho mỗi biểu thức. Kiểm tra nhiều điều kiện thường được biểu diễn dễ hiểu hơn dưới dạng cấu trúc rẽ nhánh (if statement) hoặc tái cấu trúc dưới dạng 1 biển.

***Nên***

```swift
let result = a > b ? x : y
```

***Không nên***

```swift
let result = a > b ? x = c > d ? c : d : y
```

#### 2.2.2.3. Type Annotation for Empty Arrays and Dictionaries

Với mảng và dictionary rỗng, cần ghi rõ type.

***Nên***

```swift
var names = [String]()
var lookup = [String: Int]()
```

***Không nên***

```swift
var names: [String] = []
var lookup: [String: Int] = [:]
```

#### 2.2.2.4. Short type declarations

Ưu tiên khai báo type một cách ngắn gọn hơn là cú pháp đầy đủ

***Nên***

```swift
var deviceModels: [String]
var employees: [Int: String]
var faxNumber: Int?
var dictArray: Array<Dictionary<String, AnyObject>>? or var dictArray: [[String: AnyObject]]?
```

***Không nên***

```swift
var deviceModels: Array<String>
var employees: Dictionary<Int, String>
var faxNumber: Optional<Int>
```

# Reference
Tài liệu tham khảo:
[The Swift API Design Guidelines](https://swift.org/documentation/api-design-guidelines/)
[The Raywenderlich Swift Style Guide](https://github.com/raywenderlich/swift-style-guide/)
[The Eure Swift Style Guide](https://github.com/eure/swift-style-guide/)
[The Github Swift Style Guide](https://github.com/github/swift-style-guide/)