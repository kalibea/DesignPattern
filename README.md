# DesignPattern

Aggregator   -----------> Iterator
   -                         -
   -                         -
   -                         -
 Array       ------------ ArrayIterator
   -
   -
   -
   Item(*)

iterator

Aggregator(container)
이터네이터 객체를 생성한다.
public interface Aggregator {
 Iterator  iterator();//create iterator
 }

 public interface Iterator {
   boolean next();//다음 구성 데이타가 있다면 true
   Object current();// 현재 구성 데이타를 가져온다.
 }
 구성데이타 Item

 public class Item {
    private String name;
    Private int cost;
    public Item(String name, int cost) {
       this.name = name;
       this.cost = cost;
      }
      @Override
      public String toString() {//문자열변환 자동호출메소드 
         return "("  + name + ", " + cost + ")" ;
         }
  }

  public class Array implements Aggregator {
   private Item[] items;
   public Array(Item[] items) {
    this.items = items;
    }
    //인덱스로 구성데이타를 얻어온다.
    public Item getItem(int index) {
     return items[index];
     }
     //구성데이타의 갯수를 가져온다.
     public int getCount() {
      return items.length;
      }
    @Override
    public Iterator iterator() {
     return new ArrayIterator(this);
     }
}
 public class ArrayIterator implements Iterator{
 // 컨테이너를 멤버로   가진다.
 private  Array array;
 //현재 배열에 대한 index
 //생성자로 어그리게이션을 받아와서 설정한다.
 public Arrayiterator(Array array){
    this.array = array;
    this.index = -1;// 멤버로 설정된 배열의 인덱스는 -1에서 출발한다.
    }
@Override 
 public boolean next() {
 //당연히 다음 인덱스는 현재 인덱스에서 + 1이다.
  index++
  return index < array.getCount();
}
@Override
 public Object current() {
 //현재 아이템을 리턴한다.
  return array.getItem(index);
  }
}

//실제 사용
public class MainEntry {

 public static void main(String[] args) {
 Item[] items = {
     new Item("A",10),
     new Item("B",20),
     new Item("C",30)
     };
Array array = new Array(items);//배열생성시 요소데이타를 넘겨준다.
Iterator it = array.iterator(); //배열 반복기를 생성할때 배열을 반복기의 생성자로 넘겨준다.

while( it.next() ) {
     Item item = (Item)it.current();
     System.out.printLn(item);
  }
  
}

 
     
    
 
