# 📘 Tổng hợp OOP ( Object-oriented programming ) trong JavaScript

## Đối tượng (Object) và Lớp (Class) trong OOP là gì?

### 1. Đối tượng (Object) trong OOP
Đối tượng (Object) bao gồm: Thuộc tính – Attribute (thông tin, đặc điểm của 1 đối tượng), phương thức – Method (hành vi mà đối tượng có thể thực hiện).

### 2. Lớp (Class) trong OOP
Còn lớp (Class) lại biểu thị cho một lớp bao gồm những đối tượng sở hữu những đặc tính tương tự nhau về phương thức và thuộc tính. Ví dụ một cách dễ hiểu thì: LG, Samsung,… đều là các đối tượng thuộc lớp tivi thông minh.
```html
```

Dưới đây là ví dụ tổng hợp đầy đủ các thành phần bên trong `class` trong JavaScript hiện đại (ES6+), bao gồm cả kế thừa, static, getter/setter, private field và override method.

```js
// 🔸 Class cơ bản mô phỏng người dùng
class Person {
  // 🔹 Instance field - Thuộc tính riêng mỗi object
  role = 'user';

  // 🔹 Static field - Thuộc tính dùng chung, truy cập qua class
  static type = 'Human';

  // 🔹 Private field - Chỉ sử dụng bên trong class
  #secret = 'xyz';

  // 🔹 Constructor - Khởi tạo object
  constructor(name) {
    this.name = name;
  }

  // 🔹 Instance method - Hàm gọi qua object
  speak() {
    console.log(`${this.name} speaks.`);
  }

  // 🔹 Static method - Hàm tiện ích gọi qua class
  static info() {
    return 'This is a Person class';
  }

  // 🔹 Getter - Truy cập thuộc tính như biến
  get displayName() {
    return this.name.toUpperCase();
  }

  // 🔹 Setter - Gán giá trị có kiểm soát
  set displayName(value) {
    this.name = value.trim();
  }

  // 🔹 Private method - chỉ dùng nội bộ
  #logSecret() {
    console.log(this.#secret);
  }

  revealSecret() {
    this.#logSecret();
  }
}
```

```js
// 🔸 Class kế thừa Person để mở rộng chức năng
class Student extends Person {
  constructor(name, grade) {
    super(name); // Gọi constructor class cha
    this.grade = grade;
  }

  // 🔹 Ghi đè method class cha
  speak() {
    super.speak(); // Gọi hàm speak() của class cha
    console.log(`${this.name} is a student in grade ${this.grade}.`);
  }
}
```

```js
// 🔸 Ví dụ class tổng hợp đầy đủ các thành phần nâng cao
class Example {
  // 🔹 Instance field
  property = 'instance value';

  // 🔹 Static field
  static staticProperty = 'class level';

  // 🔹 Private field
  #secret = 123;

  // 🔹 Constructor
  constructor(param) {
    this.param = param;
  }

  // 🔹 Instance method
  instanceMethod() {
    console.log('called on instance');
  }

  // 🔹 Static method
  static staticMethod() {
    console.log('called on class');
  }

  // 🔹 Getter
  get name() {
    return this._name;
  }

  // 🔹 Setter
  set name(val) {
    this._name = val;
  }

  // 🔹 Private method
  #privateMethod() {
    return this.#secret;
  }

  revealSecret() {
    return this.#privateMethod();
  }
}
```

```js
// 🔸 Thử nghiệm class Example
const ex = new Example('demo');
ex.name = 'JS';
console.log(ex.name);                  // JS
ex.instanceMethod();                   // called on instance
console.log(Example.staticProperty);   // class level
Example.staticMethod();                // called on class
console.log(ex.revealSecret());        // 123
```

```js
// 🔸 Thêm ví dụ mới: class mô phỏng tài khoản ngân hàng
class BankAccount {
  // Số dư mặc định
  #balance = 0;

  constructor(owner) {
    this.owner = owner;
  }

  // Gửi tiền
  deposit(amount) {
    if (amount > 0) this.#balance += amount;
  }

  // Rút tiền
  withdraw(amount) {
    if (amount > 0 && amount <= this.#balance) {
      this.#balance -= amount;
    }
  }

  // Xem số dư (getter)
  get balance() {
    return `${this.owner} has ${this.#balance} VND`;
  }
}
```

```js
// 🔸 Instance hoạt động
const acc = new BankAccount('Nguyen Van A');
acc.deposit(500000);
acc.withdraw(200000);
console.log(acc.balance); // Nguyen Van A has 300000 VND
```

---

## ✅ Thành phần đã bao gồm:
- `Instance field`
- `Static field`
- `Private field (#)`
- `Constructor`
- `Getter / Setter`
- `Instance method`
- `Static method`
- `Private method (#)`
- `Inheritance (extends)`
- `Super constructor & method`
- `Override method`
- ✅ Ví dụ sử dụng thực tế (BankAccount)

---
## 📋 Bảng tổng hợp các khái niệm cốt lõi

| **Thành phần**           | **Giải thích**                                                               | **Ví dụ cụ thể**                                  |
|--------------------------|------------------------------------------------------------------------------|---------------------------------------------------|
| `class`                  | Cú pháp ES6 để định nghĩa khuôn mẫu cho đối tượng                            | `class Person {}`                                 |
| `constructor`            | Hàm đặc biệt trong class dùng để khởi tạo giá trị khi tạo object             | `constructor(name) { this.name = name }`          |
| `instance`               | Một object cụ thể được tạo ra từ `class` hoặc constructor                    | `const p = new Person('Anna')`                    |
| `new`                    | Toán tử dùng để tạo một instance từ class hoặc constructor function          | `new Person('Anna')`                              |
| `function` (constructor) | Trước ES6, constructor được viết bằng function thông thường                  | `function Person(name) { this.name = name }`      |
| `prototype`              | Cơ chế kế thừa trong JS, giúp chia sẻ method giữa các instance               | `Person.prototype.sayHi = function() {}`          |
| `__proto__`              | Liên kết ngầm của object tới prototype của constructor nó được tạo từ        | `p.__proto__ === Person.prototype`                |
| Prototype Chain          | Chuỗi tìm kiếm thuộc tính theo `__proto__` nếu không có trực tiếp trên object| `p.toString()` từ `Object.prototype` nếu không có |

---

## 📘 Bảng mở rộng – Các thành phần nâng cao trong class (JS)

| **Thành phần**       | **Giải thích**                                                                  | **Ví dụ cụ thể**                                |
|----------------------|-------------------------------------------------------------------------------- |-------------------------------------------------|
| **Instance Field**   | Biến khai báo trong class, tồn tại riêng biệt trên mỗi instance                 | `property = 'value'`                            |
| **Static Field**     | Biến gắn với class, dùng chung, không truy cập qua instance                     | `static staticProperty = 'class value'`         |
| **Instance Method**  | Hàm được gán cho prototype, dùng qua object                                     | `instanceMethod() {}`                           |
| **Static Method**    | Hàm tiện ích gắn trực tiếp vào class                                            | `static staticMethod() {}`                      |
| **Getter**           | Dùng để lấy giá trị với xử lý logic khi truy cập như một thuộc tính             | `get name() { return this._name }`              |
| **Setter**           | Dùng để gán giá trị kèm logic xử lý                                             | `set name(val) { this._name = val }`            |
| **Private Field**    | Biến chỉ truy cập được bên trong class, không thể gọi từ ngoài                  | `#secret = 123`                                 |
| **Private Method**   | Hàm dùng nội bộ trong class, không thể truy cập từ bên ngoài                    | `#privateMethod() {}`                           |
| **extends**          | Từ khóa để kế thừa từ một class khác                                            | `class Student extends Person {}`               |
| **super()**          | Gọi constructor của class cha trong class con                                   | `super(param)`                                  |
| **super.method()**   | Gọi method từ class cha trong class con                                         | `super.speak()`                                 |
| **Method Override**  | Ghi đè method của class cha trong class con                                     | `speak() {}`                                    |
