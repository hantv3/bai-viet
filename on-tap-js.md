#1. DOM
- Dom là viết tắt của Document Object Model. Dùng để tương tác tìm đến các node của HTML giúp người dùng dễ dàng thay đổi giá trị và chỉnh sửa thẻ HTML.

VD:
<input type='text' value="1">

<script>
  function getValueInput(){
  let valInput =  document.querySelector('input').value;
  console.log(valInput);
  }
</script>
2. Object trong javascipt
 - Có 2 các tạo ta object trong Javascipt
 - 1 là Object Literal
Các nhận biết Object Literal trong Javascipt là Object Literal các thuộc tính và phương thức đều được ngắn cách bằng dầu phải trong ngoặc nhọn.
Lợi ích khi sử dụng Object Literal là chúng ta sẽ gom được các thuộc tính và phương thức lại cùng nhau giúp code sách và gọn hơn.
VD: tạo một object literal;

var hantv ={
  name: "Truong Van Han,
  age: 20,
  address: "Hà Nội",
  run: function(){
    console.log(`${this->name} chạy rất chậm`);
  }
}

Cách hiển thị các thuộc tính của một object literal:
console.log(hantv.name);
hantv.run();

Thay đổi và thêm giá trị vào trong đối tượng với Object Literal.

VD:
console.log(alex.childs);
var newChild = {'name': "Nam", age: 2, "address": "Phú Thọ"};
alex.childs.push(newChild);

Bên cạnh việc chúng ta có tạo object bằng {} tao cũng có thể tạo bằng các khai báo từ kháo new Object();

VD: var rabbit =  new Object();
        rabbit.name = "Thỏ tai dài";
        rabbit.age = 1;
        rabbit.color = "đen";
        rabbit.dump = function(){
          console.log(`${this.name} nhảy rất cao`);
        }
Lưu ý: Object Literal không hỡ trợ thực thể hóa đối tượng.
      Object Literal không hỗ trợ kế thừa.
- 2 là Object Constructor Function:
Là cách khai báo đối tượng sử dụng hàm tạo constructor, cộng dụng tạo ra một khuôn của đối tượng.
Ưu điểm: Có thể hiện thực hóa đối tượng.
         Có thể kế thừa.
Cách tạo đối tượng:

function Animal(name, age, color){
  // bái thuộc tính kết thúc bằng dấu ;
  this.name = name;
  this.age = age;
  this.color = color;
  this.run = function(){
    console.log(`${this.name} chạy rất nhanh`);
  }
}

Các sử dụng Object Constructor Function;

let cat = new Animal('sam', 1, 'xam');

Chúng ta có thể thêm tực tiếp một thuộc tính mới vào Object Constructor Function;

cat.gen = "mèo anh lông gắn";

Để kế thừa đối tượng của Object Constructor Function ta sử dụng phương thức call();
ý nghĩa của hàm call: là khi tạo một đối tượng mới mà muốn sử dụng các thuộc tính đã có của đối tượng cũ thì khai báo phương thức call;

VD:
function Animal(name, age, color){
  // bái thuộc tính kết thúc bằng dấu ;
  this.name = name;
  this.age = age;
  this.color = color;
  this.run = function(){
    console.log(`${this.name} chạy rất nhanh`);
  }
}


function cat(nam, age, color, gender){
  Animal.call(this, name, age, color);
  this.gender = gender;
}

- 3. Bất đồng bộ.

Để hiểu được bất đồng bộ ta phải hiệu được khái niệm xử lý đồng bộ(Synchorous), và sử lý bất động bộ (Asynchronous).

Khái niệm:

Xử lý đồng bộ: Thông thường thì code của chúng ta khi chạy thì sẽ chạy từ trên xuống dưới, và trả về giá trị của các dòng code theo thứ tự nếu có là từ 1-2-3.

Mật tốt: chương trình chạy đúng, dễ kiểm soát lỗi khi phát sinh, kiểm soát đươc logic.
Mặt bất lợi: là sẽ phải chờ, gây ra chậm việc xử lý.

Xứ lý bất đông bộ: Chường trình vẫn chạy từ trên xuống dưới đi qua hết các code nhưng kết quả trả về sẽ là đoạn code nào xử lý xong trước chả về trước, logic sẽ không chờ nhau để trả về kết quả đúng.

Mặt tốt: Tôi ưu tốc độ, giảm thời gian chờ, tạo cảm giác tốt khi người dùng trải nghiệm.

Mặt xấu: Khó kiểm soát khi phát sinh ra lỗi, không phải chương trình và đoạn code nào cũng dùng được bất đồng bộ.

Nguyên lý bất đồng bộ của javascript được dựa trên 4 thành phần:

- Call stack: Một dạng cấu trúc dữ kiệu ghi lại vị trí các câu lệnh chạy và trả về.
- WEB APIs: là luồng sử lý do trình duyệt cung cấp hay còn gọi là các hàm.
- CallBack Queue: Là một dạng cấu trúc dữ liệu quy tắc Firt-In-Firt-Out
- Event loop: Nhiệm vụ giám sát CallBack Queue có dữ liệu không, nếu có nó sẽ chạy và trả về cho call stack để hiển thị dữ liệu.

Các cách khử bất đồng bộ:
Có 3 cách khử bất đồng bộ:
- Callback: là dùng hàm để gọi một hàm khác
- Promise: là một đối tượng, nó đại diện cho một sử lý bất đồng bộ không có kết quả. Cách sử dụng promise là ta sẽ kết hợp với hàm xử lý mà nó đang đại diện;
- async/await của ES6


Json: Javascript Object Notion là kiểu dữ liệu trong javascript dữ liệu được viết trong cặm dấu ngoặc nhọn key value

Jquery (jQuey Dom Traversing) là một thư viện của javascript, nó giúp người dùng dễ xử lý và tương tác với các thẻ node html trong trang web

Ajax(Asynchronous Javascript adn XML) giúp web xử lý đồng bộ


