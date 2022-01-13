## simpledateforamt

#### simpledateformat은 시간을 원하는 포맷으로 출력해준다
#### thread safe하지 않기에 single thread상황에서는 문제가 없이 작동하지만 multi thread상황에서는 똑같은 시간이 다르게 출력될 수 있다.

#### 이를 해결하기 위해 내부에서 매번 생성하는 방법이 있다
```java
Runnable runnable = new Runnable() {
  @Override
  public void run() {
    try {
      Date date = new SimpleDateFormat("yyyy-mm-dd'T'HH:mm:ss").parse(dateString);
      System.out.println(date);
    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}
```
#### 혹은 FastDateFormat을 사용할 수 있다


      
