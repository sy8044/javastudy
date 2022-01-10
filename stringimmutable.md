## string immutable의 의미
### string pool
#### new 연산자로 생성을 하지 않았을 때 heap 내부의 string pool에 저장된다
#### new 연산자를 통해 생성하면 heap 내부에 별도의 객체에 담겨 생성된다
<pre>
<code>
String s1 = "test";
String s2 = "test"
String s3 = new String("test");
s1 == s2 // true
s1 == s3 // false
</code>
</pre>
#### 리터럴로 생성할 때 string pool에 똑같은 리터럴이 있는지 확인을 한다
#### 값 그자체를 가지는 것이 아니라 reference 값을 가지기에 똑같은 리터럴이 있으면 같은 곳을 가리킨다
#### string pool 내부의 리터럴은 immutable하게 된다
